pipeline{
    agent any
    environment { 
        DOCKER_USR_NAME = 'nageshle204'
        IMAGE_NMAE = 'webapps'
    }
        stages{
            stage ('clean WS'){
                steps{
                    script{
                        cleanWs()
          
                    }
                }
            }
            stage ('SCM')     {
                steps{
                    git 'https://github.com/Nageshcloud/maven-employee-web-application.git'
                }
            }
            stage ('BUILD') {
                steps{
                    sh 'mvn -Dmaven.test.failure.ignore=true clean package'
                }
            }
            stage ('Containerizing') {
                steps{
                    sh "docker build -t $DOCKER_USR_NAME/$IMAGE_NMAE:$BUILD_NUMBER ."
                    sh "docker tag $DOCKER_USR_NAME/$IMAGE_NMAE:$BUILD_NUMBER $DOCKER_USR_NAME/$IMAGE_NMAE:latest"
                }
            }
            stage ('push to DH') {
                steps{
                    withCredentials([string(credentialsId: 'DOCKER_TOKEN', variable: 'DOCKER_TOKEN')]) {
                     sh "docker login -u $DOCKER_USR_NAME -p $DOCKER_TOKEN"
                 
                    } 
                 sh "docker push $DOCKER_USR_NAME/$IMAGE_NMAE:$BUILD_NUMBER"
                 sh "docker push $DOCKER_USR_NAME/$IMAGE_NMAE:latest"
                }
            }
        }
    }

