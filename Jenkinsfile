pipeline{
    agent any
    environment{
        DOCKER_USERNAME = "sumittiwari2025"
        APP_NAME = "flask-app"
        IMAGE_TAG = "${BUILD_NUMBER}"
        IMAGE_NAME = "${DOCKER_USERNAME}/${APP_NAME}"


    }


    stages{
        stage('clean the workspace'){
            steps{
                script{
                    cleanWs()
                }
            }
        }

        stage('checkout git scm'){
            steps{
                git branch: 'main', url: 'https://github.com/iamsumit24/Flask_App_Cricbuzz_API.git'
            }
        }

        stage('build docker image'){
            steps{
                script{
                    sh "docker build -t ${IMAGE_NAME}:${IMAGE_TAG} ."
                }
            }
        }
        stage('Push the Image to DockerHub') {


            steps {
              withCredentials([usernamePassword(credentialsId: 'Dockercred', passwordVariable: 'pass', usernameVariable: 'user')]) {
                // some block


                    sh """
                    
                        echo ${pass} | docker login -u ${user} --password-stdin

                        docker push ${IMAGE_NAME}:"${IMAGE_TAG}"
                      


                    """
            }
            }

        }
        stage('Delete Image Locally') {

            steps {
                sh """
                    docker rmi -f ${IMAGE_NAME}:${IMAGE_TAG}
                   
                """

            }

            
        }
         
        
    }
}