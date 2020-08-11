# Dockerized Java EE project deployable server

## Environment: 
    - Server: tomcat-9.0.37, 
    - JDK: 11
    - MYSQL: 5.7
    - SFTP: atmoz-sftp

# Instructions
### Run Docker:
 - To run the docker for first time execute below command:
    ```
    docker-compose up -d --build
    ```
 - To run regularly execute below command: 
    ```
    docker-compose up -d
    ```
### Give Permission to Volumes: 
    chmod 777 -R vloumes

### Deploy Projest:
 Copy the deployable `war` file into `volumes/tomcat/deploy` directory. This `volumes/tomcat/deploy` directory is the symbolic link of `/opt/tomcat/webapps` directory. Which means tomcat will automatically detect the copied `war` file and will start deploying it.

After deploying the `war` file, `deployed-project-name.log`, `catalina.log` and others tomcat provided logs will be found in `volumes/tomcat/logs` directory. This `volumes/tomcat/logs` directory is linked with `/opt/tomcat/logs` directory.

### MySql Setup:
By changing mysql environment variables which are enlisted in `docker-compose.yml` file under `mysql` service one can easily configure `mysql database`

      MYSQL_ROOT_PASSWORD: {ROOT-PASSWORD}
      MYSQL_DATABASE: {DATABASE-NAME}
      MYSQL_USER: {DATABASE-USER-NAME}
      MYSQL_PASSWORD: {DATABASE-USER-PASSWORD}

### SFTP Setup:
This should be considered as a file server. `username` and `password` of this file server can be modified by changing `command` in `docker-compose.yml` file under `sftp-server` service. 
        
              password
                |    
    vanguard:vanguardpass:1001
       |                    |      
     username              internal server username
                          (recomended: do not change) 
     