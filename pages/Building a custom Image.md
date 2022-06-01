- [[draws/2022-04-18-15-44-15.excalidraw]]
- ````
  Layer 1. Base Ubuntu Layer
  Layer 2. Changes in apt packages
  Layer 3. Changes in pip packages
  Layer 4. Copy source code to working directory
  ```
- Command to #build images
	- `docker build . -f Dockerfile -t mumshad/mycustom-app`
- FROM, RUN, COPY and ENTRYPOINT are instructions, everything on right are arguments.
- Dockerfile is INSTRUCTION ARGUMENT file
- All Dockerfiles should start with FROM command.
- Each line of instruction creates a new layer.
- see how images are build is `docker image history _imagename_`
- Can use ARG - > a variable instruction