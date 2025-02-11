# MySQL Container Configuration

we might face situation where we need my sql not installed local. you can use the container for you advantage here.
follow the documentation for creating one.

## What is MySQL?
MySQL is widely used in web applications, especially with PHP, Java, and other backend technologies.

It stores data in tables and uses SQL for querying and managing data.

MySQL is known for its reliability, ease of use, and performance.

## Using Command Line to Run MySQL Container
- Pull the MySQL image:
    ``` bash
    docker pull mysql:latest
    ```
- Run the MySQL container:
    ``` bash
    docker run \
      --name mysql \
      -v "$(pwd)/mysql_data:/var/lib/mysql" \
      -p 3306:3306 \
      -e MYSQL_ROOT_PASSWORD=password \
      mysql:latest
    ```
  - `--name`: Name of the container.
  - `-v`: Maps the local mysql_data directory to the container's /var/lib/mysql directory for persistent storage. 
  - `--p`: Maps port 3306 on the host to port 3306 on the container (default MySQL port). 
  - `-e`: Sets the root password for MySQL.

- Stop the container:
    ``` bash
    docker stop mysql
    ```
- Start the container:
    ``` bash
    docker start mysql
    ```

- Delete the container:
    ``` bash
    docker rm mysql
    ```
## Running MySQL with Docker Compose

- Save the following configuration as docker-compose.yaml:
    ``` yaml
    version: '3.9'
    
    services:
      mysql:
        image: mysql:latest
        container_name: mysql
        ports:
          - "3306:3306"
        volumes:
          - ./mysql_data:/var/lib/mysql
        environment:
          MYSQL_ROOT_PASSWORD: password
        restart: unless-stopped
        networks:
            jelly_media_network:
               ipv4_address: 192.168.1.116 # desired ip for jellyfin
  
    networks:
      jelly_media_network:
        driver: macvlan
        driver_opts:
          parent: eth0
        ipam:
          config:
            - subnet: 192.168.1.0/24
              gateway: 192.168.1.1
              ip_range: 192.168.1.116/32
    ```
- Start the container:
    ``` bash
    docker-compose up -d
    ```
- Stop the container:
    ``` bash
    docker-compose down
    ```
## Notes
- MySQL use volumes (mysql_data) to store data persistently. If you delete the container, the data will remain intact in these directories.
- For MySQL, you can set `MYSQL_ROOT_PASSWORD` to secure the root user.
- MySQL uses port `3306` by default.
