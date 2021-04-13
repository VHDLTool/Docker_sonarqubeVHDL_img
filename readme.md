# CNES sonar-scanner / sonarqube docker image 

## Installation
1. install docker
2. get the image by running docker `pull lequal/sonarqube-vhdl:latest` and `docker pull lequal/sonar-scanner-vhdl:latest`   
For an offline installation:
   1. download the images for the [sonarqube scanner](https://github.com/VHDLTool/Docker-sonar-scanner-vhdl/releases) and the [sonarqube server](https://github.com/VHDLTool/Docker-sonarqube-vhdl/releases)
   2. import images with command : `docker load --input  sonarqube-vhdl.tar` and `docker load --input sonar-scanner-vhdl.tar`*(Please unzip the scanner image to get access to the tar file)* 
3. create a network for the two containers: `docker network create sonarbridge`   
4. launch your sonarqube instance with command : `docker run --name sonarqubeVM --net sonarbridge --rm -p 9000:9000 -e SONARQUBE_ADMIN_PASSWORD="adminpassword" lequal/sonarqube-vhdl:latest` you can change the admin password in this command line.
   you can get the sonarqube server IP with command: `docker inspect sonarbridge`
5. get the plasma example design at https://github.com/VHDLTool/Docker_sonarqubeVHDL_img/releases and unzip it
6. execute the command `docker run --net sonarbridge --rm  -e SONAR_HOST_URL="http://172.18.0.2:9000" -v "$(pwd):/usr/src" lequal/sonar-scanner-vhdl:latest` in the folder with your VHDL code (same location as the `sonar-project.properties` file).Be careful to change the server IP address with the one extracted at step 4.
7. access to sonarqube at the address http://localhost:9000 

*Note* by default all the implemented rules are enabled. That is to say CNES default ones and its derivated NXE. As some rules are duplicated, so issues will be. Please create a custom quality profile to select which rule you want to be checked (and remove doubles).
 
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
* follow the associated readme for [server](https://github.com/VHDLTool/Docker-sonarqube-vhdl/blob/develop/README.md#developers-guide) and [scanner](https://github.com/VHDLTool/Docker-sonar-scanner-vhdl/blob/develop/README.md#developers-guide)
* You can export the images with the commands `docker save --output sonarqube-vhdl.tar lequal/sonarqube-vhdl:latest   ` and `docker save --output sonar-scanner.tar lequal/sonar-scanner-vhdl:latest `

