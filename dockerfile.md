# Dockerfiles

## What is a Dockerfile?
- A Dockerfile is a text file that contains a set of instructions on how to build a Docker image.
- It defines everything needed to create an image for a container, such as...
  - what image base to use
  - what files to copy
  - what commands to run
  - what ports to expose

## How does a Dockerfile work?
1. **Build phase** - ```docker build``` will read the instructions in the Dockerfile to create an image.
2. **Run phase** - ```docker run``` will run the image. This creates a container based on the image and executes the commands in the CMD or ENTRYPOINT.

## What does a Dockerfile look like?
1. ```FROM``` specifies the base image to use. It's the starting point for your custom image.
  - ex: ```FROM ubuntu:20.04```
2. ```COPY``` and ```ADD``` copies files or directories from your local system to the image.
  - ex: ```COPY index.html /usr/share/nginx/html/```
3. ```RUN``` executes commands *inside* the image while it's being built, i.e. installing packages or configuring the environment.
  - ex: ```RUN apt-get update && apt-get install -y curl```
4. ```EXPOSE``` exposes a port to make it accessbile from otuside the container (not mandatory, but useful).
  - ex: ```EXPOSE 80```
5. ```CMD``` and ```ENTRYPOINT``` define the command that will run when a container starts from the image.
  - ex: ```CMD ["nginx", "-g", "daemon off;"]``` (for running nginx)

## Example Dockerfile:
```
# Use an official nginx image as the base
FROM nginx:latest

# Copy your custom HTML file to the container
COPY index.html /usr/share/nginx/html/index.html

# Expose port 80 (default for nginx)
EXPOSE 80

# Command to run the nginx server
CMD ["nginx", "-g", "daemon off;"]
```

