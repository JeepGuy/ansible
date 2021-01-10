# Set up Docker for Ansible

Docker uses an internal network
 172.17.0.x
 
## Find an image that you like. 
- Ensure that ssh is enabled

docker pull image

docker pull centos:centos7.7.1908

### Start docker image in the background

docker run -it -d image:tag

docker run -it -d centos7.7.1908

### Find the ip address of the machine

docker inspect <first two letters of the image id>

IPAddress": "172.17.0.2

 Run the docker command two more times for three instances.
 




