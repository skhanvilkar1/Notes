- **Bridge Network**
	- Internal private network, containers are automatically assigned to it usually in the series of 172.17.0.1 network range.
	- Containers are automatically assigned IPs are connected to Bridge network and can communicate with each other.
	- To access containers from outside world, map ports of container to ports of host, making it accessible via Hosts IP address and mapped port no.
	- E.g. ` docker run ubuntu`
- **Host Network**
	- Containers are directly mapped to Host's network.
	- E.g. `docker run --network=host nginx`
- **None**
	- This network type completely isolates the containers in the Docker host
	- E.g. `docker container run --network=none nginx`
- **User Defined Network**
	- User can define their own network, besides the default bridge network
	- Command example - `docker network create --driver bridge --subnet 182.18.0.0/16 custom-isolated network`
	- check using `docker network ls`
	- [[draws/2022-05-19-23-10-14.excalidraw]]
	- **Embedded DNS**
	-
- **Embedded DNS**
	- Does not work with default bridge network
	- **only works with user defined network**
	- Embedded DNS helps containers resolve each other by their name
	- IP address is not useful
	- **DNS server** is **127.0.0.11** usually in Docker host
	- note that embedded DNS WORKS ONLY WITH USER-DEFINED NETWORK
	- Cannot use internal IPs for communication, as its not ideal, its not guaranteed that container will get same IP when it reboots
	- All containers in docker host can resolve each other with the name of the container. Docker has a build in DNS server (of sorts) at 127.0. 0.11
	- How does docker implement Networking -?
		- Docker uses network namespaces. Described later
- **Important commands**
	- How do we see existing IP address etc assigned to particular network ? --> Run command `docker container inspect container name`
	- `docker network ls` --> list default networks
	- `docker container network inspect` container_id or name of container --> see ip address assigned to a network under IPAM (IP address management)
	- To connect a custom network to container use --> `docker network connect custom-net my-container`
	- You may connect a single container to multiple networks
	- `docker network disconnect custom-net my-container`
	- `docker network rm custom-net`   /deletes the network
	- `docker network prune`    /removes all un-used networks, only works on user-defined not default
-
- **Networking Deep Dive - Namespaces**
	- What are namespace - > If your host is a house, each private room is a namespace. Child can see only his/her room. As a parent you may have visibility inside this namespace room if you wish. Parent has control to establish connectivity between rooms (namespaces)
	- Process namespace - container thinks it is his own host, underlying host can see the process.
	- To test above use ps aux under container and on host
	- Create a Network Namespace
	  1. `ip netns add red` & `ip netns add blue` 
	  2. check or list host interfaces - `ip link`
	  3. `ip netns exec red ip link` ---> executed inside red namespace
	  4. As of now there is no connectivity between the Namespace of networks , so lets create a link (pipe) like an virtual cables
	  5. run command `ip link add veth-red type veth peer name veth-blue`
	  6. To attach each interface to name space --> `ip link set veth-red netns red` & i`p link set veth-blue netns blue`
	  7. Now assign ip addresses to namespaces. Use ip addr command --> for red -> `ip -n red addr add 192.168.15.1 dev veth-red` for blue -> `ip -n blue addr add 192.168.15.2 dev veth-blue`
	  8. Now once ip addresses are assigned, bring them up
	  `ip -n red link set veth-red up`
	  `ip -n red link set veth-blue up`
	- **Diagram**
		- [[draws/2022-05-25-22-41-58.excalidraw]]
	-
	- Once done, you can see that you are able to ping each namespace from another
		- `ip netns exec red ping 192.168.15.2`
		- `ip netns exec red arp` & `ip netns exec blue arp`  // here we can see both have learnt each others arp addresses.
	- if you check host arp addresses - > ip arp -> host has no idea of Namespaces and its arps.
	-
	- What if there are many namespaces ? How will they communicate?
	- You need a virtual switch within the host -> Multiple ways 
	  a. Linux Bridge (native) 
	  b. OpenvSwith (custom product)
	- To create an internal bridge network -> we add a new link of type bridge --> `ip link add v-net-0 type bridge`
	- This is just another interface and will appear in `ip link`  output
	- `ip link set dev v-net-0 up` --> brought new link/interface created up
	- This is an interface for host but acts like a switch for namespaces inside the host.
	- Now to connect namespaces to to this switch -> Need new cables, connect all namespaces to this switch now instead of each other as shown above diagram
	- Delete the link created above first.
	- `ip -n red link del veth-red` -> when you delete one interface of link other is auto deleted
	- `ip link add veth-red type veth peer name veth-red-br` --> new link for red namespace
	- `ip link add veth-blue type veth peer name veth-blue-br` -> same for blue ns
	- Now to add one end to red namespace and other to bridge --> 
	  `ip link set veth-red netns red`
	  `ip link set veth-red-br master v-net-0`
	- Run same for blue namespace accordingly.
	- Assign ip addresses same as before and bring it up
	  `ip -n red addr add 192.168.15.1 dev veth-red`
	  `ip -n blue addr add 192.168.15.2 dev veth-blue`
	  `ip -n red link set veth-red up`
	  `ip -n blue link set veth-blue up`
	-
	- What if I try to reach one of these interfaces from the host? It will not work try -> ping 192.168.15.1
	- What if you want to establish connectivity between host and NSs? Remember that the switch is the network interface (virtual) on the host , so you can assign an IP address to v-net-0 switch /interface created
	- `ip addr add 192.168.15.5/24 dev v-net-0`
	- We can now ping any namespace from local host.
	- Diagram
		- [[draws/2022-05-25-23-03-24.excalidraw]]
	- This is still private network, we cannot reach outside world or outside world to us.
	- Only door is eth0 or interface of host.
	- Routing table has no information of outside world
	- So to find gateway to outside world - here there is only one possiblity - > eth0 which is the interface on local host. Local host is Gateway
	- add routes to namespace , e.g. add route in blue namespace to reach outside network of 192.168.1.0
	  `ip netns exec blue ip route add 192.168.1.0/24 via 192.168.15.5` .5 is v-net-0 address
	-
	- Now when you ping `ip netns exec blue ping 192.168.1.3` you do not get destination unreachable but no response is received either
	-
-