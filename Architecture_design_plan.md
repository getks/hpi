# Plan

#####  1. Create Dockerfile for each microservice, S1, S2 and S3
       - Dockerfile pulls latest debian image
       - Exposes the required port say, 5000
       - Install all the pre-requisites
       - Define ENV Variables
       - copy & execute the required config/scripts from your local env to docker
       - choose the WORKDIR
##### 2. Build & tag image and push to docker repository
        - docker build -t s1:latest .
##### 3. Push to docker repository (do the same for all microservices)
        - docker login
        - docker tag s1 khushboo30/s1:v1.0.1
##### 4. Now, we have the images of icroservices, which we can deploy anywhere in our infrastructure.
##### 5. Create a docker-compose file and define all the 3 services in a network, with port definitions and ENV variables.
         Sample docker-compose:
```sh
version: "3"
services:
  s1:
    image: khushboo30/s1:v1.0.0
    deploy:
      replicas: 1 
      restart_policy:
        condition: on-failure
    ports:
      - "5000:5000"
    networks:
      - ms_cluster 
    volumes:
      - /data/s1:/data/s1
    environment:
      DB_IP: 
	  DB_PORT:
    entrypoint: [  ]
  s2:
    image: khushboo30/s2:v1.0.0 
    deploy:
      replicas: 1 
      restart_policy:
        condition: on-failure
    ports:
      - "5001:5001"
    networks:
      - ms_cluster
    volumes:
      - /data/s2:/data/s2
    environment:
      DB_IP:
	  DB_PORT:
    entrypoint: [  ]
  s3:
    image: khushboo30/s3:v1.0.0
    deploy:
      replicas: 1
      restart_policy:
        condition: on-failure
    ports:
      - "5003:5003"
    networks:
      - ms_cluster
    volumes:
      - /data/s3:/data/s3
    environment:
      DB_IP:
	  DB_PORT:
    entrypoint: [ "" ] 

networks:
  ms_cluster:
```

##### 6. Set up an AWS account, and install terraform.
        On AWS console, use the region nearest to your location, create a new IAM user which has admin rights besides root user, get ACCESS_KEY_ID and SECRET_ACCESS_KEY
        and save it in a secure location for eg: keepass.
        Use AWS_ACCESS_KEY_ID and AWS_SECRET_ACCESS_KEY as environment variables for terraform in order to be able to use terraform with AWs account.
        
##### 7. Start creating Terraform code in its .tf files.
        

      
          
