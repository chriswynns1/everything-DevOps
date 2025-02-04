# Docker / Kubernetes

## Docker:

### What is Docker?
- Docker lets you package applicatins and their dependencies into containers.
- Containers are lightweight and portable. They ensure your application runs the same way, regardless of the environment.

### Resources: 
- [Play with Docker](https://www.docker.com/play-with-docker/)

### Key Concepts:
- Images: a template for a container.
  - Read-only package that has everything needed to run an app.
  - Static; they don't change when you run them.
  - Stored in registries like Docker Hub or your local machine.
  - Like a cooking recipe.

- Containers: a running instance of an image.
  - A live, isolated process on your system.
  - Mutable; they can change state, store files, and run apps.
  - Multiple containers can run the same image.
  - Like a cooked meal.

You can cook multiple meals from the same recipe, just like you can run multiple containers from the same image.

### Cheatsheet:
```docker --version``` will check the docker version.
```docker images``` will list all downloaded images.
```docker run -it ubuntu bash```
  - ```-it``` = interactive mode
  - ```ubuntu``` = image name
  - ```bash``` = the command that runs inside the container.
- ```docker rm hello-world``` removes the container.
- ```docker rmi nginx``` will remove the image from the repo.
```docker ps``` will check running containers.
```docker logs hello-world``` will display logs from a detached container (in this case, "hello-world").
```docker attach hello-world``` will reattach a running container.
```docker pull nginx``` downloads the nginx image, but does not run it.
```docker exec -it hello-world sh``` will connect to hello-world's shell.
```docker run -d --name hello-world -p 8080:80 nginx```
  - Starts a container named "hello-world", running in detached mode (-d).
    - Foreground mode (default):
      - Runs the container **attached** to your terminal.
      - You will see all logs and outputs in the terminal.
      - If you close the terminal, the container stops.
    - Detached mode: runs the container in the background, **detached** from the terminal.
      - Logs will not appear (unless you check them manually).
      - The container will continue to run after the terminal is closed.
  - The container maps 8080 on *your* machine to port 80 in the container.
  - Visting http://localhost:8080 will show the nginx welcome page.
