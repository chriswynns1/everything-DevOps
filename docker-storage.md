# Docker Storage

## Volumes
- Containers are ephemeral (they lose data once stopped).
- **Volumes** are a way to persist data outside of the container so it's not lost when the container is removed.
  - Volumes are stored **on the host machine**.

## Create and Run a Container w/ a Volume:
```
docker run -d --name volume-test -v my-volume:/data ubuntu
```
- ```-v my-volume:/data``` will create a **named volume** (```my-volume```) and mount it to the ```/data``` directory *inside* the container.
- ```ubuntu``` is the base image.

To check to see if the volume was created successfully, we can execute the container in interactive mode to use bash.
```
docker exec -it volume-test bash
```
The ```-it``` command tells docker to run the container in interactive mode. ```volume-test``` is just the name of the container. ```Bash``` is the command to be executed.
