pipeline{
    agent any
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
                    sh 'docker build -t sample:0.1.0 .'
                }
            }
        }
    }

