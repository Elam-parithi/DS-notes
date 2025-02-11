# MongoDB Container Configuration
If you don't have internet access you can not access the mongoDB cloud server. 
which gives access to free tier for users. It also makes a limitation. here you can use containers for your leverage.

## What is MongoDB?
MongoDB is a NoSQL database that stores data in a flexible, JSON-like format. It’s great for applications that require scalability and flexibility in handling unstructured data.

MongoDB is a document-oriented database that provides high performance, high availability, and easy scalability.

It is widely used in modern web applications, especially those built with Node.js, Python, and other frameworks.

MongoDB stores data in collections (similar to tables in SQL) and documents (similar to rows in SQL).

## Using Command Line to Run MongoDB Container
- Pull the MongoDB image:

  ``` bash
  docker pull mongo:latest
  ```
- Run the MongoDB container:

  ```bash
  docker run \
    --name mongodb \
    -v "$(pwd)/mongo_data:/data/db" \
    -p 27017:27017 \
    -e MONGO_INITDB_ROOT_USERNAME=admin \
    -e MONGO_INITDB_ROOT_PASSWORD=password \
    mongo:latest
  ```
  - --name: Name of the container.
  - -v: Maps the local mongo_data directory to the container's /data/db directory for persistent storage.
  - -p: Maps port 27017 on the host to port 27017 on the container (default MongoDB port).
  - -e: Sets environment variables for the root username and password.

- Stop the container:

  ``` bash
  docker stop mongodb
  ```
- Start the container:

  ``` bash
  docker start mongodb
  ```
- Delete the container:

  ```bash
  docker rm mongodb
  ```
## Running MongoDB with Docker Compose
Save the following configuration as docker-compose.yaml:

  ``` yaml
  version: '3.9'
  
  services:
    mongodb:
      image: mongo:latest
      container_name: mongodb
      ports:
        - "27017:27017"
      volumes:
        - ./mongo_data:/data/db
      environment:
        MONGO_INITDB_ROOT_USERNAME: admin
        MONGO_INITDB_ROOT_PASSWORD: password
      restart: unless-stopped
      networks:
            jelly_media_network:
               ipv4_address: 192.168.1.115 # desired ip for jellyfin
  
    networks:
      jelly_media_network:
        driver: macvlan
        driver_opts:
          parent: eth0
        ipam:
          config:
            - subnet: 192.168.1.0/24
              gateway: 192.168.1.1
              ip_range: 192.168.1.115/32
  ```
- Start the container:
  ```bash
  docker-compose up -d
  ```
  
- Stop the container:
  ```bash
  docker-compose down
  ```
  
## notes
  - MongoDB use volumes (mongo_data) to store data persistently.
  - For MongoDB, you can set `MONGO_INITDB_ROOT_USERNAME` and `MONGO_INITDB_ROOT_PASSWORD` to create a root user.
  - MongoDB uses port `27017` by default. 
  - Always use strong passwords for root users.