# Deploy On Server

# Table of Contents
1. [What is this document](#purpose)
1. [Steps](#steps)

---
# What is this document <a name="purpose"></a>
Steps to deploy a java project on server

# Steps <a name="steps"></a>
1. Create jar: first of all we need to create a jar file for the spring boot project that we want to deploy
    - open terminal 
    - go to the project folder and run this command
    ```
        mvn clean package -P dev
    ```
    - Rename the jar file as: tenantAuthServer.jar
1. Connect VPN (optional)
1. Connect to server using FileZilla (mac) / putty (windows)
1. Upload jar file to the location 
    - Location: /root/ADAC/tenant
1. ssh into server from terminal
    - ssh root@10.162.255.174
    - when prompted enter password: rzpVTMPzl44Z
1. Delete: nohup.out (optional)
    - application logs will be written in this nohup.out file. if it exists already, we might want to delete it so at the time of deployment a fresh file gets created and we can see the fresh logs. However this is an optional step. If we do not delete the file, new logs will get appended to the end. 
    ```
        rm -rf nohup.out
    ```
1. Kill already running process
    - search the process
    ```
        ps aux|grep tenantAuthServer_9097
    ```
    - Kill if there is an running process
    ```
        kill -9 pid <pid>
    ```
1. Run sh file
    - There should be two files in the deployment folder - 1. jar file to deploy, 2. shell script that will trigger the jar file. 
    - Go to the deployment location and run below command to execute the shell script
    ```
        ./tenantAuthServer.sh
    ```
    - If the shell script does not work for permission issue, here is the fix: 
    ```
        chmod -R 777 ./
    ```
    - Sample .sh file
    ```
    #!/bin/sh
    #nohup java -jar tenantAuthServer_9094.jar &
    nohup java -Dserver.port=9097 -jar authserver.jar --spring.config.location=file:///root/ADAC/gtm/application.yml &

    ```
1. Test APIs:
    - http://10.162.255.174:9096/oauth/token
    - http://10.162.255.174:9096/api/v2/scim/organization
    - http://10.162.255.174:9096/swagger-ui.html#/



#### Swagger URL: http://localhost:9097/swagger-ui/index.html?configUrl=/v3/api-docs/swagger-config#/


# Reference Links:
### How to deploy spring boot application on external Tomcat Server
- https://www.youtube.com/watch?v=IucUnTqJhiE