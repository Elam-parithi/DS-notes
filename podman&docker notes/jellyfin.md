
# Jellyfin container configuration

Initially I used pen and paper or notepad++ to take notes. 
But after I found about jellyfin it was very useful to store videos and play it in browser.
I gathered all the videos from my course and store it locally for faster access. 
Nowadays 5G unlimited is available. but I'm still using 4G with limited data.

Additionally, who else can be the best teacher than time and yourself. I record short videos myself and store it here.
which will be useful when recalling it. I usually get board when watching YouTube video tutorials again and again.
but here it is different it is never boring to watch the videos and recall it.

you can also use locally install on windows and linux, but it will lose compute power to keep it running all the time.
I have repurposed my old broken laptop for this purpose only.

So here is hot to use it in docker.

## What is jellyfin ?
- As per [jellyfin.org](https://jellyfin.org/) it is a "The Free Software Media System.
Jellyfin is the volunteer-built media solution that puts you in control of your media. 
Stream to any device from your own server, with no strings attached. Your media, your server, your way."

- There are other opensource media management tools like plex. 
If you know how to use `OpenVPN` you can use it to stream your notes anywhere on earth.

- jellyfin also supports `https` locally.

- supports following.
  - videos
  - images
  - audio
  - pdf
  - ebooks
    

## Using command line to run a docker (simplest way):

- first `pull` the container from the internet (download).
    ``` 
    docker pull jellyfin/jellyfin 
    ```
- Run the computer locally
    ```
    docker run \
      --name jellyfin \
      -v "$(pwd)/cache:/cache" \
      -v "$(pwd)/config:/config" \
      -v "$(pwd)/media:/media" \
      -p 80:8096 \
      jellyfin/jellyfin:latest
    ```
  - `--name`: for name of the container.
  - `-v`: for creating volume were the data will be stored locally.
    - if you don't create the `media` volume the videos will not be available on the website.
    - I stored my videos in folder named 'media' locally. pointing to the same name or different name on container side. 
    - It can be different you are going to log in and manually assign folder. can also be multiple volumes. 
    - `cache` and `config` where users configuration and passwords and appdata stored. 
    - **_If volume is not created for cache and config it will be required to reconfigure every time you start it_**.
  - default port is 8096. I'm mapping it to 80 on host side.
  - finally container name`jellyfin/jellyfin:latest` 
- stopping the container:
    ```bash
    docker stop jellyfin
    ```
- starting the configured container
    ```bash
    docker start jellyfin
    ```
- listing the containers
  - listing the running container
    ```bash
    docker ps 
    ```
  - listing with stopped container but not deleted yet.
    ```bash
    docker ps -a
    ```
- deleting the container
    ``` bash
    docker rm jellyfin
    ```
  - if you delete the container it will not delete the caches it will be there. 
  - you can recreate the container with the same passwords and configuration.

## Running with docker-compose

This is the easiest way to run a docker container once it was configured. 
Without docker-compose knowledge it is hard to configure.

- Here is the docker-compose file. save it as exactly `docker-compose.yaml`
    ``` yaml
    version: '3.9'

    services:
      jellyfin:
        image: jellyfin/jellyfin:latest
        container_name: jellyfin
        ports:
          - "80:80"     # for use at starting without SSL
          - "443:443"   # with SSL ceritificate.
        volumes:
          - ./config:/config  # Configuration files
          - ./cache:/cache  # Cache files 
          - ./media:/media  # Media files
        restart: unless-stopped
        networks:
          jelly_media_network:
             ipv4_address: 192.168.1.114 # desired ip for jellyfin

    networks:
      jelly_media_network:
        driver: macvlan
        driver_opts:
          parent: eth0
        ipam:
          config:
            - subnet: 192.168.1.0/24
              gateway: 192.168.1.1
              ip_range: 192.168.1.114/32
    ```
- To start the file
    ``` bash
    docker-compose up -d
    ```
    - If no error received you docker is up and running.
    - don't use `-d` on running first time. Because you will get your default password here first time.
    - login with `192.168.1.114:80` and set root password.
    - set the folders on library. It is only available on admin privileges.
- To stop the file
    ```bash
    docker-compose down
    ```

## notes:

- you can set an ip address to you ip using host file
    - file is on 
      - `C:\Windows\System32\drivers\etc\hosts`. open with administrator privileges in windows.
      - `/etc/hosts` on linux
    - set your desired ip address and name
      ``` text
      192.168.1.114  myjellyfin.website
      ```
      port is not used here. only on address bar.
- you can also create SSL and install it locally using OpenSSL.