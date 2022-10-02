pipeline {
    agent any
    stages {  
        stage('Docker Build') {
            steps {
                script {
                    sh 'docker build -t petclinic:latest .'
                    sh "docker tag petclinic:latest rcartifacoty.jfrog.io/petclinic-docker-local/petclinic:${BUILD_NUMBER}"
                    sh 'docker images'
                }
            }
        }
        stage ('Push image to Artifactory') { // take that image and push to artifactory
        steps {
            rtDockerPush(
                serverId: "jfrog",
                image: "rcartifacoty.jfrog.io/petclinic-docker-local/petclinic:${BUILD_NUMBER}",
                targetRepo: 'petclinic-docker-local',
                properties: 'project-name=petclinic;status=stable'
            )
        }
    }
        stage ('Pull image from Artifactory') { // take that image and push to artifactory
        steps {
            rtDockerPull(
                serverId: "jfrog",
                image: "rcartifacoty.jfrog.io/petclinic-docker-local/petclinic:${BUILD_NUMBER}",
                sourceRepo: 'petclinic-docker-local'
            )
        }
    }
        stage ('Run docker image') {
            steps {
                script {
                    sh 'docker images'
                    sh """
                        set +e
                        docker stop petclinic
                        set +e
                        docker rm petclinic
                        set +e
                        """
                        sh "docker run --name petclinic -d -p 8083:8080 rcartifacoty.jfrog.io/petclinic-docker-local/petclinic:${BUILD_NUMBER}"
                }
            }
        }                 
    }
}
