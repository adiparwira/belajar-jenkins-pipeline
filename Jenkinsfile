pipeline {
    agent none
    environment {
        AUTHOR = "Aryadi"
        EMAIL = "adiparwira@yahoo.com"
        WEB = "https://chat.openai.com"
    }
    stages {
        stage('Prepare'){
            environment {
                APP = credentials('adi-cred')
            }
            
            agent {
                node {
                    label "Linux && Java11"
                }
            }
            
            steps {
                echo "APP USER: ${APP_USR}"
                echo "APP PASSORD: ${APP_PSW}"
                sh 'echo "APP Password: $APP_PSW > pass.txt"'
                echo "AUTHOR: ${AUTHOR}"
                echo "Start job: ${env.JOB_NAME}"
                echo "Start build: ${env.BUILD_NUMBER}"
                echo "Branch name: ${env.BRANCH_NAME}"
            }
        }
        stage('Build'){
            agent {
                node {
                    label "Linux && Java11"
                }
            }
            
            steps {
                script {
                    for (int i = 0 ; i < 10 ; i++) {
                        echo("Script ${i}")
                    }
                }
                
                echo("Start build")
                sh("./mvnw clean compile test-compile")
                echo("Finish build") 
            }
        }

        stage('Test'){
            agent {
                node {
                    label "Agent && 2"
                }
            }
            
            steps {
                echo("Start test")
                sh("./mvnw test")
                echo("Finish test")
            }
        }

        stage('Deploy'){
            agent {
                node {
                    label "Agent && 2"
                }
            }
            
            steps {
                echo 'Hello Deploy 1'
                sleep(5)
                echo 'Hello Deploy 2'
                echo 'Hello Deploy 3'
            }
        }
    }

    post {
        always {
            echo "I will always say Hello again"
        }

        success {
            echo "Hore success"
        }

        failure {
            echo "wow no error"
        }

        cleanup {
            echo "Don't care suucess of error"
        }
    }
}
