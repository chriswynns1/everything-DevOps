# Docker Storage

## Volumes
- Containers are ephemeral (they lose data once stopped).
- **Volumes** are a way to persist data outside of the container so it's not lost when the container is removed.
  - Volumes are stored **on the host machine**.

## Create and Run a Container w/ a Volume:
```
docker run -d --name volume-test -v my-volume:/data nginx:latest
```
- ```-v my-volume:/data``` will create a **named volume** (```my-volume```) and mount it to the ```/data``` directory *inside* the container.
- ```nginx:latest``` is the base image.

To check to see if the volume was created successfully, we can execute the container in interactive mode to use bash.
```
docker exec -it volume-test bash
```
The ```-it``` command tells docker to run the container in interactive mode. ```volume-test``` is just the name of the container. ```Bash``` is the command to be executed.

Now that we've entered the command line for the container, we can change some data in the /data directory:
```
cd /data
echo "persistent data" > /data/impo.txt
```
If we remove the container (but not the volume) and run a new container with the same volume, the data will persist.
```
docker rm -f volume-test
docker run -d --name new-volume-test -v my-volume:/data nginx:latest
docker exec -it new-volume-test bash
cd /data/
ls
```
You should see the "impo.txt" (or whatever you decided to name it)
