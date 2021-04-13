# CNES sonar-scanner / sonarqube docker image 

## Installation
1. install docker
2. download the images for the [sonarqube scanner](https://github.com/VHDLTool/Docker-sonar-scanner-vhdl/releases) and the [sonarqube server](https://github.com/VHDLTool/Docker-sonarqube-vhdl/releases)
3. import images with command : `docker load --input  sonarqube-vhdl.tar` and `docker load --input sonar-scanner-vhdl.tar`*(Please unzip the scanner image to get access to the tar file)* 
4. create a network for the two containers: `docker network create sonarbridge`   
   you can inspect IPs parameters with command: `docker inspect sonarbridge`
5. launch your sonarqube instance with command : `docker run --name sonarqubeVM --net sonarbridge --rm -p 9000:9000 -e SONARQUBE_ADMIN_PASSWORD="adminpassword" lequal/sonarqube-vhdl:latest` you can change the admin password in this command line.
   you can inspect IPs parameters with command: `docker inspect sonarbridge`
6. execute the command `docker run --net sonarbridge --rm  -e SONAR_HOST_URL="http://172.18.0.2:9000" -v "$(pwd):/usr/src" lequal/sonar-scanner-vhdl:latest` in the folder with your VHDL code .Be careful to change the IP address with the one extracted at step 4.
7. access to sonarqube at the address http://localhost:9000  
 
## Creation
These image are modified version of CnesCat lab:
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
<<<<<<< HEAD
* follow the associated readme for [server](https://github.com/VHDLTool/Docker-sonarqube-vhdl/blob/develop/README.md#developers-guide) and [scanner](https://github.com/VHDLTool/Docker-sonar-scanner-vhdl/blob/develop/README.md#developers-guide)
* You can export the images with the commands `docker save --output sonarqube-vhdl.tar lequal/sonarqube-vhdl:latest   ` and `docker save --output sonar-scanner.tar lequal/sonar-scanner-vhdl:latest `
=======
* execute in a terminal `docker build -t vhdltool/sonar-sonarqube-vhdl .` and `docker build -t lequal/sonar-scanner-vhdl .` for each repository.

You can export the images with the commands `docker save --output sonar-sonarqube-vhdl.tar vhdltool/sonar-sonarqube-vhdl:latest` and `docker save --output sonar-scanner-vhdl.tar lequal/sonar-scanner-vhdl:latest `
>>>>>>> 169dd9f6a79dd0bf2e6046148d620bb0e43f1850
