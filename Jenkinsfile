pipeline {
    agent any
    stages {
        stage('Docker Build') {
            steps {
                script {
             
                    sh 'sudo docker build -t petclinic:latest .'
                    sh 'sudo docker images'
                }
            }
        }
        stage('Docker Run') {
            steps {
                script {
                    sh 'sudo docker run -d -p 8083:8080 petclinic'
                }
            }
        }
    //     stage ('Push image to Artifactory') { // take that image and push to artifactory
    //     steps {
    //         rtDockerPush(
    //             serverId: "jfrog",
    //             image: ARTIFACTORY_DOCKER_REGISTRY + "/petclinic:latest",
    //             //host: 'tcp://localhost:2375',
    //             targetRepo: 'petclinic', // where to copy to (from docker-virtual)
    //             // Attach custom properties to the published artifacts:
    //             properties: 'project-name=docker1;status=stable'
    //         )
    //     }
    // }                 
    }
}
