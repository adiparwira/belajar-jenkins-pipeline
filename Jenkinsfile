pipeline {
    agent {
        label "Linux && Java11"
    }
    stages {
        stage('Build'){
            steps {
                echo("Start build")
                sh("./mvnw clean compile test-compile")
                echo("Finish build") 
            }
        }

        stage('Test'){
            steps {
                echo("Start test")
                sh("./mvnw test")
                echo("Finish test")
            }
        }

        stage('Deploy'){
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