# Spring Boot App - deployment & containerization  
Simple university project built for deployment and containerization of a Spring Boot App using Ansible and Docker.   


## Table of contents
- [General Info](#general-info)  
- [Technologies used](#technologies-used)
- [Usage](#setup-and-usage)
- [Notes](#notes)

## General Info
The purpose of this project is to demonstrate a practical use of Ansible in combination with Docker learned throughout the course of "Infrastructure Programming".  
The targeted Web Application this project uses is [another university project](https://github.com/hristijankocev/mcil) I made using Spring Boot.   

Ansible playbooks functionality shortly described:  
1. Install the *lean_delivery* ansible galaxy role on the control node needed for installing JDK  
> It is expected that the web app won't be delievered as a .jar file, which is why we need to install JDK on the remote servers for packaging the app with maven. Yeah, not the best practice.  
2. Install git and clone web app repository on the remote server
3. Install JDK on the remote server
4. Install, start and test docker on the remote server
5. Package the web app with maven and run it in docker with `docker compose`
6. Test connections to the containerized web app  

*[Dockerfile](https://github.com/hristijankocev/MCIL/blob/master/Dockerfile)* and *[docker-compose.yaml](https://github.com/hristijankocev/MCIL/blob/master/docker-compose.yml )* are already included in the spring boot app github repository.    
Dependencies of the web app are Selenium and Postgresql, for which we have separate containers created with the docker-compose file.
 
## Technologies used
- Ansible 2.9
- Docker

## Setup and Usage  
`$ git clone https://github.com/hristijankocev/mcil-ip` on your ansible control node  

`$ cd mcil-ip/`  
> modify the inventory based on where you want the web app to be delievered  
   
`$ ansible-playbook site.yaml -i hosts -K --ask-pass`  

If all of the tasks finished without errors, the web app should be available on all of the hosts in the webservers group of the inventory, i.e. http://remote-server:8080/  
## Notes
The playbook intended for installing and testing Docker is right now only working for CentOS distributions. Docker already provides a [script](https://get.docker.com) for easy and automated installation on any distribution, but I have not used it only because I wanted to install and configure it manually for testing and learning purposes.
