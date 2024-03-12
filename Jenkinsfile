pipeline {
    agent any
    environment{
        IMAGE_NAME = "proyecto-final"
        CONTAINER_NAME = "pf-cont"
    }
    stages{
        stage('Build Docker Image'){
            steps{
                script {
                    try {
                        sh "docker image rm ${IMAGE_NAME}"
                    } catch(err){} finally {
                        sh "docker build . -t proyecto-final"
                    }
                }
            }
        }
        stage('Kubernetes Configuration') {
            steps {
                script {
                    sh "kubectl apply -f k8s-config/*.yaml"
                }
            }
        }
        // stage('Kubernetes Deploy'){
        //     steps {
        //         script{
        //             try {
        //                 sh "docker stop ${CONTAINER_NAME}"
        //                 sh "docker rm ${CONTAINER_NAME}"
        //             } catch(err){} finally {
        //                 // sh "docker run -d -p 9080:80 --name ${CONTAINER_NAME} ${IMAGE_NAME}"
        //             }
        //         }
        //     }
        // }
    }
}

// def getDockerTag(){
//     def tag  = sh script: 'git rev-parse HEAD', returnStdout: true
//     return tag
// }
