```
docker --version                        # Check installed Docker version
docker info                             # Display system-wide Docker information

docker pull <image_name>                # Download a Docker image from Docker Hub
docker images                           # List all available images
docker rmi <image_id>                   # Remove a specific image
docker rmi $(docker images -q)          # Remove all images

docker build -t <image_name> .          # Build an image from a Dockerfile
docker run <image_name>                 # Run a container from an image
docker run -d <image_name>              # Run a container in detached mode
docker run --name <container_name> <image_name>  # Run a container with a custom name
docker run -p 8080:80 <image_name>      # Map port 8080 of the host to port 80 in the container

docker ps                               # List running containers
docker ps -a                            # List all containers (including stopped ones)
docker stop <container_id>              # Stop a running container
docker start <container_id>             # Start a stopped container
docker restart <container_id>           # Restart a container
docker rm <container_id>                # Remove a container
docker rm $(docker ps -aq)              # Remove all stopped containers

docker logs <container_id>              # View logs of a container
docker exec -it <container_id> /bin/sh  # Access a running container (Linux shell)
docker exec -it <container_id> cmd      # Access a running container (Windows CMD)
docker inspect <container_id>           # Get detailed information about a container

docker compose up                       # Start services defined in docker-compose.yml
docker compose up -d                    # Start services in detached mode
docker compose down                     # Stop and remove all services

docker network ls                        # List all Docker networks
docker network create <network_name>     # Create a new Docker network
docker network connect <network_name> <container_id>  # Connect a container to a network
docker network disconnect <network_name> <container_id>  # Disconnect a container from a network

docker volume ls                         # List all Docker volumes
docker volume create <volume_name>       # Create a new volume
docker volume rm <volume_name>           # Remove a volume
docker volume inspect <volume_name>      # View volume details
docker system prune                      # Remove unused containers, networks, and images


### Dockerfile Commands ###
FROM <base_image>                   # Set the base image (e.g., Ubuntu, Node.js, Golang)
LABEL maintainer="Your Name"        # Add metadata to the image
RUN <command>                       # Execute a command during the image build
COPY <src> <dest>                   # Copy files from local machine to the container
ADD <src> <dest>                    # Similar to COPY but can extract archives
WORKDIR <path>                      # Set the working directory in the container
ENV <key>=<value>                   # Define environment variables
EXPOSE <port>                        # Declare the container's network port
CMD ["executable", "arg1"]          # Default command executed when container starts
ENTRYPOINT ["executable", "arg1"]   # Set the main application that runs inside the container
VOLUME ["/data"]                     # Create a mountable directory
ARG <var_name>                       # Define build-time variables
HEALTHCHECK --interval=30s CMD curl -f http://localhost || exit 1  # Health check for container
USER <username>                      # Set the user for running the container

### Example Dockerfile ###
FROM node:16
LABEL maintainer="Your Name"
WORKDIR /app
COPY package.json .
RUN npm install
COPY . .
EXPOSE 3000
CMD ["node", "server.js"]

### Docker Compose Commands ###
docker compose up                   # Start services defined in docker-compose.yml
docker compose up -d                # Start services in detached mode
docker compose down                 # Stop and remove services
docker compose restart               # Restart all services
docker compose ps                    # List running services
docker compose logs                  # Show service logs
docker compose build                 # Build images for services
docker compose stop                  # Stop running containers
docker compose rm                    # Remove stopped services

docker compose exec <service> <cmd>  # Execute a command in a running container
docker compose run <service> <cmd>   # Run a command in a new container

docker compose pull                   # Pull latest images for services
docker compose config                 # Validate the compose file syntax

docker compose scale <service>=3      # Scale a service to multiple instances

### Example Docker Compose File (docker-compose.yml) ###
version: '3.8'
services:
  web:
    image: node:16
    working_dir: /app
    volumes:
      - .:/app
    ports:
      - "3000:3000"
    command: ["node", "server.js"]
  db:
    image: postgres:latest
    environment:
      POSTGRES_USER: user
      POSTGRES_PASSWORD: password
      POSTGRES_DB: mydatabase
    volumes:
      - pgdata:/var/lib/postgresql/data
volumes:
  pgdata:
  
```

