Jenkins Pipeline CI/CD for spring-petclinic

Step1: Dockerizing the app
I have used two images

1. maven:3.6.3-jdk-11-slim - to build a package file
2. openjdk:11-jre-slim - to run the package

To run the dockerized app locally follow these steps
- Build image locally using

- $ docker build -t petclinic .
- $ docker run -d -p 8080:8080 petclinic


Jenkinsfile
1. Install docker on the jenkins server
2. Wrote a declarative jenkinsfile
3. Created a pipeline in the jenkins
