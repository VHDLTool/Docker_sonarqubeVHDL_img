# CNES sonar-scanner / sonarqube docker image 

## Installation
1. install docker
2. download the image  sonar-sonarqube.tar from the release page.
3. import images with command : `docker load --input sonar-sonarqube.tar` and import the scanner image from docker hub:https://hub.docker.com/r/lequal/sonar-scanner-vhdl with command `docker pull lequal/sonar-scanner-vhdl`

4. create a network for the two containers: `docker network create sonarbridge`   
   you can inspect IPs parameters with command: `docker inspect sonarbridge`
5. launch your sonarqube instance with command : `docker run --name sonarqubeVM --net sonarbridge --rm -p 9000:9000 -e SONARQUBE_ADMIN_PASSWORD="adminpassword" lequal/sonarqube-vhdl:latest` you can change the admin password in this command line.
   you can inspect IPs parameters with command: `docker inspect sonarbridge`
6. execute the command `docker run --net sonarbridge --rm  -e SONAR_HOST_URL="http://172.18.0.2:9000" -v "$(pwd):/usr/src" lequal/sonar-scanner` in the folder with your VHDL code .Be careful to change the IP address with the one of your  
7. access to sonarqube at the address http://localhost:9000  
 
## creation
These images are modified version of CnesCat lab:
* sonarqube     : https://github.com/cnescatlab/sonarqube.git 
* sonar-scanner : https://github.com/cnescatlab/sonar-scanner.git

The cnescatlab version was adapted to include:
* Sonarqube VHDL plugins coming from :
    * https://github.com/VHDLTool/sonar-coverage-ghdl
    * https://github.com/VHDLTool/sonar-coverage-modelsim
    * https://github.com/VHDLTool/sonar-fpga-metrics-plugin 
    * https://github.com/VHDLTool/sonar-VHDLRC

The dockerfiles to create docker images including vhdlRC are locate at:
* https://github.com/VHDLTool/Docker-sonar-sonarqube
* https://github.com/VHDLTool/docker-sonar-scanner

To create the docker image do:
* clone each previous project
* install docker
* execute in a terminal `docker build -t vhdltool/sonar-sonarqube .` and `docker build -t lequal/sonar-scanner .` for each repository.

You can export the images with the commands `docker save --output sonar-sonarqube.tar vhdltool/sonar-sonarqube:latest` and `docker save --output sonar-scanner.tar lequal/sonar-scanner:latest `
