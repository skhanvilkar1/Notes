- Managing Azure Active Directory
  collapsed:: true
	- How to use Azure to secure your identities and understand how users and groups are implemented in Azure AD.
	- Azure Active Directory
	  collapsed:: true
		- Cloud based identity and directory management service enabling access to Azure services and other SaaS solutions like Microsoft 365, DropBox, Salesforce etc.
		- Self service options like password reset, authentication, SSO, device management, hybrid identities etc. On-prem applications etc.
		- AD concepts
			- Identity  - Object that can be authenticated. User, group or service principals (service accounts)
			- Account - Associate data attributes to an identity we call it account. Example location, department and phone number of user makes that identity an Account.
			- Azure AD Account  - Accounts created in Azure AD is called Azure AD account
			- Azure AD Tenant or directory - Dedicated instance of Azure AD that is created during sign up of any Microsoft cloud service subscription. Tenant and Directory means same. We can have one or multiple directories based on requirement.
		- Azure AD vs Active Directory Domain Services (ADDS)
		  collapsed:: true
			- Two different services. Installing ADDS in Azure is not Azure AD
			- Azure AD is cloud based or web based , so its queried using HTTP or HTTPS. ADDS using LDAP protocol for querying
			- AZ AD uses SAML, WS-Federation, Open ID and OAuth for authorization. ADDS uses KERBEROS for authentication
			- AZ AD Federation can be set up with 3rd party providers like Facebook v/s ADDS , Federation is only to other domains, 3rd party not supported.
			- Azure AD is managed service offering v/s ADDS will run on VMs or Physical Windows Servers.
		- Azure AD Editions
			- Premium P2 - No directory object limit, Single Sign on, B2B collab, O365 access, Hybrid identities, Conditional access, identity Protection, Identity Governance.
			- Premium P1 -No directory object limit, Single Sign on, B2B collab, O365 access, Hybrid identities, Conditional access
			- M365 Apps - No directory object limit, Single Sign on, B2B collaboration, O365 access
			- FREE - included with Azure Subscription - No directory object limit, Single Sign on, B2B collaboration.
		- User Accounts
		  collapsed:: true
			- User accounts are used for authentication and authorization.  All users must have an account
			- Each user can have optional properties.
			- All users can be accessed from Azure Active Directory > USERS > All users
			- We can perform bulk operations like bulk create, bulk invite and bulk delete.
			-
			- Types of Identities -
			- Cloud Identities - Users exist only in  internal Azure AD or external Azure AD
			- Guest Users - Exist outside of Azure , Microsoft accounts, Live Accounts etc.
			- Directory synchronized users - These users are synchronized from your on-prem Windows AD. We cannot create directory synchronized users (obvious)
			- REFER USER CREATION LAB HERE IN AZURE AD.
			-
		- User Accounts - Bulk Operations 
		  collapsed:: true
			- Bulk operations will let you download a CSV template where you add users you want to create, delete or invite.
			  BULK CREATE
			  BULK INVITE
			  BULK DELETE
			  BULK DOWNLOAD
			- Azure Active Directory > Users - you will see Bulk Operations option, download CSV Template
			- You can restore DELETED users by going to Users > Deleted users option
	- Azure AD Join
	  collapsed:: true
		- We can uses Azure AD join to manage our corporate assets (similar to domain join in ADDS)
		- IT admins make sure devices are secure and follow security standards
		- Azure AD join offers SINGLE SIGN ON - app services and SAAS solutions
		- Provides Access to Microsoft Store for Business
		- Enterprise state Roaming - sync all your config across devices
		- Windows Hello - Sign in using biometric or facial sign in
		- Device Management - Admins can check complaince and restric
		- On-prem Access - Seamless access to on-prem apps and leverage single sign on
	- Self-Service Password Reset (SSPR)
	  collapsed:: true
		- Enables users to reset password without need to call IT helpdesk
		- Setup Multiple methods to reset
		- Premium P2 license
		- Enable for all users or targeted users
		- Admin accounts - enabled by default. 
		  
		  STEP 1 - Enable SSPR for all or targeted users
		  STEP 2 - Set up number of authentication methods required for reset of password
		  STEP 3 - Users will be requested to register for SSPR next time login and enable reset method
		-
		- REFER SSPR LAB Azure Active Directory > Password Reset > go to properties , options available none, selected, all
		- If a user wants to setup up his/her profile , they can go to aka.ms/ssprsetup and they will be able to setup their SSPR reset options. Methods available are Authenticator app / phone etc.
		- If user wants to reset password they can go to --> aka.ms/sspr > redirects to passwordreset.microsoftonline.com
		-
		-
	- Group Accounts
	  collapsed:: true
		- Security groups -> assign a role, inherited by all users of group
		- MS 365 groups -> offers collab. opportunities
		  
		  Membership Assignment Types
		- Assigned - default
		- Dynamic users - attribute of users changed, AZ will check and modify/remove
		  --> Check Dynamic Membership rules under group. specify your query/expression here
		- Dynamic device - will dynamically check device properties and will remove if attributes match remove rule. Not available for MS 365 groups
		-
	- Multi-Tenant Environments
	  collapsed:: true
		- Each Tenant or directory represents an organization. An org can have one or more tenants.
		- Azure AD there is no parent child relationship
		- Each Azure AD org is fully independent. Each tenant is considered separate
		- Resource Independence - Creation and deletion of resource in one Tenant does not have any impact on another tenant.
		- Administration independence - Level of permission of user account is only valid within the tenant
		- Synchronization independence - Each Azure AD Tenant's synchronization of accounts can be independently set up for each tenant.
		- Default domain provided yourorg.onmicrosoft.com , you can bring your custom domain names need to set up DNS
		- You can switch between directories (tenants)
		- You need an invite from Tenant admin to join another Tenants.
	-
- Azure Subscriptions
  collapsed:: true
	- Need subscription to create resources. All charges of all resources made are charged to subscription.
	  Hence Azure subscription acts like a billing boundary for usage.
	- Resources deployed are mapped to Azure Subscription
	- Help us set up environmental boundaries - Dev, TEST , QA etc
	- Every subscription has unique subscription ID.
	- An account can have multiple subscriptions
	- Any identity part of Azure AD or trusted MS Cloud service can sign up for a subscription.
	- Different types
		- Enterprise Agreements - 500 or more users and devices. Offers services and licensing at discounted rates. Pre payment required
		- Pay-as-you-go subscription - Ideal for small size org. Monthly billing
		- CSP - Cloud Solution Provider - Licensed by microsoft partner. managed by Microsoft partners
		- Free Trial - $200 credit for 30 days and free limited access for 12 months
		- Azure for Students
		- Visual Studio subscription
	- Subscription can act as scope of access management and policy governance.
	-
	-
	- Understanding Hierarchy
		- Management Groups -> offers a scope above subscriptions by which you will be able to group subscriptions together
		- Root Management group is created by default and you have upto 6 levels of nested groups excluding the root group.
		- Each subscription can contain one or more resources.
		- Hierarchy helps in implementing polices 
		  Management Groups (can have nested groups, excluding root up to 6 levels)> Subscriptions > Resource Groups > Resources
	- RBAC (Role Based Access Control) - administrators to grant access to Azure resources
		- Three questions 1. Who? 2. What? (role definition, what ops can be performed) 3. Where ? (where we want to provide the access, defines boundaries) >> Role assignment .
		  **Max 2000 role assignments in each subscription**
		- Follow principle of Least privilege
		- Build-in roles - Owner, Contributor, Reader and there are custom roles
		- Scope  -> role assigned at Management groups get inherited to its Subs, to its resources groups and down to resources. It trickles down
		- AZURE RBAC vs AZURE AD ROLES
		  ````
		  | Azure RBAC                                                                  | Azure AD Roles                                                                     |
		  |-----------------------------------------------------------------------------|------------------------------------------------------------------------------------|
		  | Used to manage access to AZ resources                                       | Used to manage AZ AD features                                                      |
		  | Scope includes managment groups, subscriptions, resource groups, resources  | Scope is at AZ AD Tenant level                                                     |
		  | Role assignment can be managed via Azure Powershell Azure CLI ARM Templates | Roles can be managed via Azure Portal MS365 admin Microsoft Graph API              |
		  | Examples include Owner Contributor, Reader, User Access Administrator       | Examples include Global Administrator, Billing Administrator, Global Reader, etc.  |
		-
		- ![image.png](../assets/image_1665480398277_0.png)
	- Built-in Roles -> Offered by Azure. 100s of build in roles.
		- Four fundamental roles 
		  1. Owner -> Gives full access to all resources, and can delegate access to other people.
		  2. Contributor -> All access but cannot delegate
		  3. Reader -> Read access to all resources 
		  4. User Access Administrator -> Able to give users access to different Azure resources
		- There can be scenarios where we cannot use fundamental roles
		  We can fine tune roles called custom roles here
		- Can be done by AZ CLI, REST API, AZ PowerShell, Azure Portal
		- Each directory can have 5000 custom roles
		- We can assign custom roles to users, groups, service principals to any scope.
- **Azure Tags**
  collapsed:: true
	- Adding metadata to our subscription groups, resource groups and resources
	- Helps in logically filter out our resources for management purposes.
	- No. of characters is limited to 512 characters, values is limited to 256. Max tags allowed 50.
	- Cost management - Tags can be used to filter Azure usage and cost management. Tags added to resources propagated to billing system.
	- Go to resource (object) you want to tag and add a tag.
	- ![image.png](../assets/image_1665970143273_0.png)
	- You can use tags to filter as well.
	- Use CLI or PowerShell to automate tagging.
	- We can make tags inherited only by using Azure policies , by default its not. Only tags at resource levels can be used in billing level
- **Resource locks**
  collapsed:: true
	- Avoids accidental changes.
	- Support inheritance
	- Read only locks -> cannot be modified
	- Delete locks -> Ideal for resources you want to modify but do not delete
	- Resource groups > Locks > Add lock
	- Inherited to all resources inside Resource Group.
- **Analyzing cost**
  collapsed:: true
	- Azure Cost Management to analyze cost
	- Cost Analysis, Can connect AWS Cost
	- Budget and recommendations
	- Export data to CSV , schedule reports
- **Cost Savings**
  collapsed:: true
	- Azure Reserved Instances (RI) -> pay upfront for 1 or 3 years
	- Azure Hybrid Benefit -> (AHUB) -> license cost cheaper
	- Credits -> Visual Studio Enterprise / Professional
	- Regions pricing is different , but should not violate compliance or performance workloads
	- You can set Budgets
	  ![image.png](../assets/image_1665970930554_0.png)
	- You can create budgets , export budgets and reports etc.
- **Azure Policies** -> create manage and assign policies , to achieve compliance 
  collapsed:: true
	- Four points
	  1. Definition is a JSON document which is used to fine policy and its effect. 
	  2. Scope
	  3. Assignment -> process of assigning a policy
	  4. Compliance -> evaluate compliance
	- Usecases
		- Allowed resource types
		- Allowed Virtual machine SKUs -> users can only use set no. of types of VM skus
		- Allowed locations -> Define set of cloud locations where we can deploy resources
		- Require Tags -> enforce tags
		- Inherit tags
		- Allowed resource groups locations
		- Not a complete list here
	- Initiative
		- ![image.png](../assets/image_1665971370672_0.png)
		- chain these policies together and assign as single unit called Azure Initiative.
		- Policy takes precedence. Takes around 30 mins to take effect.
		- How to valuate compliance --> go to policy pane
- **Virtual Networks**
	- Basic fundamental building resource of Azure
	- Representation of cloud Network. AZ Virtual Network helps us create and manage networking in Auzre
	- Dedicated instance
	- Hybrid scenarios
	- Connectivity between Azure Service and Azure VMs and enables AZ VMs to connect internet.
	- **Virtual network Concepts**
	  collapsed:: true
		- Needs a subscription to create a VNET (Subscription > Region > VNet)
		- Next we need a Region. Region represents a set of datacenters which are part of different availability zones.
		- Within the region we can create Azure VNET , Each virtual network we create should have a address space. Can be Private or Public. Do not let Azure address space overlap with your on-prem or virtual network
		- Subnet -> Subnet helps us to sgement VNet address space to smaller group.
	- **Private IP addresses**
	  collapsed:: true
		- Used within AZ VNet and hybrid scenarios including VPN Gateway and ExpressRoute connections
		- Allocation methods
		  1. Static allocation - Does not change even if instance is rebooted 
		  2. Dynamic IP addressing - Dynamically allotted to address pool.
	- **Public IP addresses**
	  collapsed:: true
		- With help of public addresses we can use with interfacing with Public Internet and AZ services
		- Allocation Types - Static & Dynamic
		- SKU : Basic and Standard 
		  | Feature       | Basic SKU                                                                        | Standard SKU                                                       |
		  |---------------|----------------------------------------------------------------------------------|--------------------------------------------------------------------|
		  | IP Allocation | Static / Dynamic                                                                 | Static                                                             |
		  | Security      | By default, open                                                                 | By default, closed                                                 |
		  | Resources     | Virtual Machines NIC, VPN Gateways,  Public Load balancers, Application Gateways | Virtual Machine NICs,  Public Load Balancers, Application Gateways |
		  | Redundancy    | No zone redundancy                                                               | Zone redundant                                                     |
		- Azure reserves 5 IP addresses in each network, Reserved IPs are used for Network address, Default gateway, 2 for DNS and 1 for broadcast
		- To create Public address , go to Public IP addresses
		  ![image.png](../assets/image_1665973885536_0.png)
	- **User Defined Routes**
	  collapsed:: true
		- What are System Routes -> created by default
		  1. Communication between VMs in the same subnet
		  2. Communication between VMs in different subnets in same virtual Network (VNet)
		  3. Communication from VM TO INTERNET -> But by default blocked by Network policy.
		  4. Site-to-Site communication using VNet gateways
		- User-Defined Route
			- Route tables help you to define User Defined Routes
			- NVA - Network Virtual Appliance
		-
		-
	- Service Endpoints 
	  collapsed:: true
		- We may have to maintain a list of public address to access storage accounts (example). So hard to maintain a whitelist
		- When we switch to Service Endpoint -> you can directly add workload private IP subnet
		- Better security
		- Leverages Microsoft Backbone network
		- Ease of Setup and management.
		- Bottom line - A service exposed via a Public IP address on your Azure network can be accessed by your other AZ services (any network), without themselves having to configure a public IP
		- ![image.png](../assets/image_1666073623984_0.png)
	- **Private Link**
	  collapsed:: true
		- Above example , destination is always public.
		- We create a private endpoint, which communicates with exposed public endpoint destination via a private link . VM feels it connects to private endpoint
		- Traffic remains in micrsoft network
		- Seamless integration with on-prem and peered networks
		- Eliminates risk of data exfiltration
		- Direct availability in Azure VNets.
		  ![image.png](../assets/image_1666073942285_0.png)
		- True Private connectivity.
		- When we create a private endpoint , it automatically creates a DNS zone and its is attached to our virtual network so instead of resolving to public ip, your destination resolves to private IP via DNS
	- **Azure DNS**
	  collapsed:: true
		- Easy service to host DNS solutions
		- Able to do DNS hosting, create multiple records
		- Zone name should be unique within resource group.
		- Delegated DNS zones in on-prem that can provide AZ DNS servers for name resolution
		- Records sets -> max allowed is 20 and need to be unique.
		- Azure DNS is a global service
		- >> check DNSData View.
	- **Private DNS Zones**
		- Name resolutions for services deployed on Azure Virtual Network
		- Implement name resolution across VNets.
		- This is also a global service. only metadata needs resource location.
		- we can establish name resolution in our Virtual Networks. common DNS Zones
		- Just for name resolution and not communication between Networks!!
	- ^^Network Security Groups^^
		- Network Security groups are called NSG.
		- With help of NSG we can **filter** traffic , operates at layer 4 and allows to filter
		- **Rule sets** - NSG comprises a set of priority based rules that can be used to allow or deny inbound or outbound traffic
		- **Association** -> NSGs can be associated to subnets and network interfaces. You can associate _multiple_ subnets and network interfaces to single NSG
		- **Evaluation**  -> NSGs applied at subnet and network interface as evaluated separately. 
		  Traffic requires "allow" rule at both levels to be admitted.
		- ^^Network Security Groups Rules^^
		  collapsed:: true
			- Rules are evaluated based on priority.
			- Default priority can be overriden with high priority rules.
			- 65000 number and onwards rules cannot be modified
			- 100 to 64999 allowed to be written. Lower number higher priority
		- Effective Security Rules
		  collapsed:: true
			- Effective -> based on evaluation of nic and subnet level NSGs
			- Read about service tags  (?)
		-
		-
	- Azure Firewall
		- Highly scalable and available - taken care by Azure
		- Layer 7 firewall as a service
		- Redundancy - spans multiple Availability zones.
		- Multiple types of rules supported - Network rules, NAT rules, Application rules
		- Threat Intelligence - Deny traffic from and to malicious IP addresses
		- Support Multiple Public IPs
		- Azure firewall needs a dedicated subnet, as it needs to scale for freedom of scaling
		- place firewall in central virtual network , acting like a hub (hub and spoke model
		- Can be extended to on-premises network as well
	-