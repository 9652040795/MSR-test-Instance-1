created the instance of  t2.micro and Operating System instances Ubuntu Server 16.04 LTS
connected to the instance through SSH keys
#-------Hostname change--------------------
changed the host name # to know the hostname  # $ hostname
Edited the hostname and the hostfiles # sudo vi /etc/hostname
sudo vi /etc/hosts
changed the second line that starts with 127.0.0.1
---------------software package installation-----
installed the required packages with apt module
----------------create container-------------
created the docker container structure 
mkdir dockercompose && cd dockercompose
$ mkdir webapp
$ echo "<h2>It Works</h2>" > webapp/index.html
Created Dockerfile for Webapp
$ vim  webapp/Dockerfile
add following content


version: '3'
services:
  db:
     image: mysql
     container_name: mysql_db
     restart: always
     environment:
        - MYSQL_ROOT_PASSWORD="secret"
  web:
    image: apache
    build: ./webapp
    depends_on:
       - db
    container_name: apache_web
    restart: always
    ports:
      - "8080:80"
Build Webapp Image
$ docker-compose build
#For web container it uses webapp/Dockerfile to build an image
Launch Docker Containers
docker-compose up -d
Update Content in Web Application
$ echo "Welcome to Docker" >> webapp/index.html
$ docker-compose build
$ docker-compose up -d
http://dockerhost:8080/  #access your web application on port 8080 of docker host machine. You will see the updated content here

