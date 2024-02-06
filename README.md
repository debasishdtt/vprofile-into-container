<h1 align="center" id="title">VPROFILE project container</h1>

<p align="center"><img src="https://socialify.git.ci/debasishdtt/vprofile-project-container/image?name=1&amp;owner=1&amp;theme=Light" alt="project-image"></p>

## 🌐 Project Overview
<p>In this web application project users will access the system via a browser or app by specifying the load balancer's IP address. 
  The load balancer powered by Nginx will route incoming requests to an Apache Tomcat server which is a popular choice for hosting Java web applications. 
  The user-created program is hosted on the Tomcat server with NFS servers providing optional external storage support. A MySQL database service stores user 
  login information where Memcached serves the caching purpose and a dummy RabbitMQ service (a message broker) is supplied for practice and possible 
  future connection with functional services simplifying data streaming and interconnecting applications within the system.</p>
<h5>🌟About</h5>
This project was developed as part of a guided project/tutorial on Udemy by Imran Teli. It serves as a practical exercise to reinforce the concepts learned during the tutorial.

## 🎯 Project Objectives
* Set up a local development environment for a multi-service stack.
* An infrastructure as code that can be simply deployed and reused using Vagrant and scripting.
* Set up real-world projects locally and automatically for extensive R&D.

## 💻 Built with
* Hypervisor: Oracle VM Virtual Box
* Automation: Vagrant
* Command Line Tool: Git Bash
* IDE (Optional): Visual Studio Code.

## 📚 Prerequisites
* JDK 11
* Maven 3 or later
* MySQL 5.6 or later

## 🔧 Technologies
* Spring MVC
* Spring Security
* Spring Data JPA
* Maven
* JSP
* MySQL
* Docker

## 🏛️ Architectural Design
* Load Balancer: Nginx is employed to handle load balancing, efficiently routing incoming requests to our Apache Tomcat server.

* Web Server: Apache Tomcat, a popular Java web application service, hosts the developer's application.

* Database Caching: Memcached for a distributed caching system for speeding up dynamic web applications.

* Database: MySQL database service is used to store user login details securely.

* Message Broker: A dummy RabbitMQ service is included in this project, though non-functional, to introduce complexity and provide practice for future integration.

![application stack](https://github.com/debasishdtt/vprofile-project/assets/81139107/37d494c3-6ec8-4864-b0fd-564936fc9eff)
<p align="center">Fig. 1: Architectural design of the setup</p>

<h3>To Run</h3>
Using your local machine, execute the following states:

Get the Docker images by using the provided link to access Docker Hub.

Load the Docker Compose file.

Navigate to http://localhost:8080 in the browser to access the application.

<h3>Docker Compose</h3>
This Docker Compose 3.8 configuration file runs a multi-container application. It supports MySQL, Redis, Memcached, RabbitMQ, an application container, and an HTTP server. The "vprodb" service setups a MySQL container, forwards port 3306, and stores data in the "vprodbdata" volume. "redis" uses an official Redis image, "vprocache01" uses Memcached, and "vpromq01" uses RabbitMQ with specified port configurations. The "vproapp" service creates an application container on port 8080 and stores data in "vproappdata". Finally, the "vproweb" service forwards port 80 to a web server container. The VProfile application's components are built on these containers, ensuring scalability and modularity in Dockerized environments.

~~~
version: '3.8'
services:
  vprodb:
    build: 
      context: ./Docker-files/db
    image: arupgope/vprofiledb
    container_name: vprodb
    ports:
      - "3306:3306"
    volumes:
      - vprodbdata:/var/lib/mysql
    environment:
      - MYSQL_ROOT_PASSWORD=vprodbpass
  redis:
    image: "redis:alpine"

  vprocache01:
    image: memcached
    ports:
      - "11211:11211"

  vpromq01:
    image: rabbitmq
    ports:
      - "15672:15672"
    environment:
      - RABBITMQ_DEFAULT_USER=guest
      - RABBITMQ_DEFAULT_PASS=guest


  vproapp:
    build: 
      context: ./Docker-files/app
    image: arupgope/vprofileapp
    container_name: vproapp
    ports:
      - "8080:8080"
    volumes:
      - vproappdata:/usr/local/tomcat/webapps


  vproweb:
    build: 
      context: ./Docker-files/web
    image: arupgope/vprofileweb
    container_name: vproweb
    ports:
      - "80:80"


volumes:
  vprodbdata: {}
  vproappdata: {}

~~~

## 💡 Outcome Showcase
<img width="960" alt="Screenshot_1" src="https://github.com/debasishdtt/vprofile-project-container/assets/81139107/6e2b0965-c54e-47f1-b5dd-48db23be6231">
<p align="center">Fig. 2: Accessing from web</p> 
<img width="963" alt="Screenshot_3" src="https://github.com/debasishdtt/vprofile-project-container/assets/81139107/6aa654e5-2517-4f57-9cef-ac2c9ec8ea63">
<p align="center">Fig. 3: Data from DB</p> 
<img width="961" alt="Screenshot_4" src="https://github.com/debasishdtt/vprofile-project-container/assets/81139107/ccec8dce-3017-44b5-9b08-37fc49aa8754">
<p align="center">Fig. 4: Data is cached</p> 

## 🌱 Room for Growth

