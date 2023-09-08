# Docker_Vprofileapp
containerizing vprofile application on Docker 
- **Vprofile Application Stack**: we have many services
    - Nginx, Tomcat, Memcache, RabbitMQ, Mysql
- When we say Docker as a tool - means not only docker engine also docker-compose and docker_hub to host our images.

**Steps to Implement:**

**Part -I**

Steps to set up our stack services

Find the right Base image from dockerhub

Write a Dockerfile to customize Images.

Write docker-compose.yml file to run multi containers.

Test it & Host Images on Dockerhub

**Part - II: project workflow**

- Fetch the source code from Git repo
- write Dockerfile for services to customization (3 dockerfiles - nginx, tomat, mysql)
    - in Dockerfile, we get 3 base images form docker hub
- Then Docker Build command which will execute on docker engine -  it will read the Dockerfile and build the image for you.
- Docker-compose: Once docker images are ready, we use docker compose. we mention all the containers with the images and then test it.
- Docker hub: Once they tested fine then we are pushing our customized images to docker hub in our docker account.

**Part -III: Setup Docker Engine on Proxmox cluster**

1. Installed Ubuntu VM(22.04) on Proxmox, remotely accessing through terminal - ssh
    - ip, - 10.0.20.199
    - to ssh - ssh satya@10.0.20.199
2. Installing Docker engine on ubuntu vm from **docs.docker.com/engine/install/ubuntu**
    1. Before installing docker engine, 1st setup apt repository - you are installing some dependencies to apt
        1. sudo apt-get update
        sudo apt-get install ca-certificates curl gnupg
    2. add docker GPG key:
        1. sudo install -m0755 -d /etc/apt/keyrings
        2. curl -fsSL https://download.docker.com/linux/ubuntu/gpg| sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
        3. sudo chmod a+r /etc/apt/keyrings/docker.gpg
    3. add the repo to Apt sources: 
        1. echo \
          "deb [arch="$(dpkg --print-architecture)" signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
          "$(. /etc/os-release&& echo "$VERSION_CODENAME")" stable"| \
          sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
        2. sudo apt-get update
    4. Install Docker packages
        1. `$ sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin`
        2. sudo docker run hello-world
