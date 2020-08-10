# docker-tomcat-mysql-sftp 
### docker-mocker for local server

## Environment: 
    Server: tomcat-9.0.37
    JDK: 11
    MYSQL: 5.7
    SFTP: atmoz-sftp

## Requirements
    docker
    docker-compose

## Instructions
 ### To run the docker for first time execute below command:
    docker-compose up -d --build
 ### To run regularly execute below command: 
    docker-compose up -d
 ### Execute below command for accessing 'volumes' directory: 
    chmod 777 -R vloumes

## Foot Note
#### * Configure MYSQL
#### * Configure SFTP
#### * Deploy Path : `volumes/tomcat/deploy`
#### * Log Path : `volumes/tomcat/logs`




```N:B: If it helps put a star. Thanks.```
