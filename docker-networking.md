# How does Docker networking work?

## Basics
- Docker uses **network namespaces** to isolate network resources between containers.
- Containers get their own IP addresses and communicate w/ each other securely.

## Drivers
- bridge (default for containers on a single host)
- host (use the host's network)
- overlay (multi-host networking in Swarm mode)
- macvlan (assigns MAC addresses to containers)
- none (complete isolation)

## Default Network
- The default network = **bridge** network
  - Network driver for containers that are running on a single host
  - Containers on the same bridge can communicate with each other using their container names / IP addresses
  - Containers in *different* bridge networks are isolated.
```
docker network create my-bridge-network
docker run -d --network my-bridge-network --name container1 nginx
docker run -d --network my-bridge-network --name container2 nginx
```
These containers will be able to communicate.

## Host Network
- uses the host's network stack directly.
- Containers **share** the host's IP address; they can access the host network interfaces directly.
- Faster, less isolated than the bridge network.
```
docker run --network host nginx
```
This container gets the host's IP address.

## No Network
- If you need a container to *not* have access, this is how you do it.
```
docker run --network none nginx
```

## Container Network
- Containers share the network namespace of another container.
```
docker run -d --name container1 nginx
docker run -d --name container2 --network container:container1 nginx
```
Container2 will share container1's network stack / use the same IP.

## Custom Network (User-defined Bridge Network)
- If you need automatic DNS resolution (containers refer to each other by name) then use this.
```
docker network create --driver bridge my-custom-network
docker run -d --network my-custom-network --name container1 nginx
docker run -d --network my-custom-network --name container2 nginx
```
These containers can refer to each other by their names.

## Network Isolation
- Containers are isolated from each other by default.
- A container on network-a CANNOT communicate w/ a container on network-b.
- You can connect containers to multiple networks to allow for communication between them.

## Recap:
- Containers on the same network can talk to each other using their names automatically.
- Containers on **different** networks cannot communicate (unless you explicitly allow it, i.e. connecting the container to multiple networks).
  - Or, expose a port on a container to the host machine (```-p```) to allow external communication.
 
