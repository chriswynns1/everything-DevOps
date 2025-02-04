# Docker Compose

## What is it?
- Allows you to define and manage multi-container Docker applications in a simple YAML file.
- Simplifies running multiple containers that need to work together.
- The entire stack goes into a YAML file.

## Key Components:
- ```docker-compose.yml``` is the main file with all of your services (containers, networks, volumes, settings).
- **Services:** each container in Docker Compose is referred to as a **service**.
  - A group of containers can also be a service.
  - You define this in the ```docker-compose.yml``` file.

## Example:
```
version: '3'
services:
  web:
    image: nginx:latest
    ports:
      - "8080:80"
    networks:
      - webnet
  db:
    image: mysql:latest
    environment:
      MYSQL_ROOT_PASSWORD: example
    networks:
      - webnet
    volumes:
      - db_data:/var/lib/mysql

networks:
  webnet:
    driver: bridge

volumes:
  db_data:
    driver: local
```

## Cheatsheet:
- ```docker-compose up``` starts your application (in the terminal).
- ```docker-compose up -d``` runs it in the background.
- ```docker-compose down``` stops and removes the containers, networks, and volumes created by ```docker-compose up```.
- ```docker-compose logs``` shows the logs from all running services.
- ```docker-compose up --scale web=3``` will create 3 instances of the ```web``` service.
  - You can scale up or down with however many services you need.
- ```docker-compose exec web bash``` will open a shell (bash) on the web container.

## Why do I need to learn Docker Compose?
- You can define all of your services (i.e. frontend, backend, DB) in a single file.
- Spin them up together.
- Saves time and hassle of setting each container up individually.
