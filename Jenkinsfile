pipeline {
    agent none
    options {
        disableConcurrentBuilds()
        timeout(time:5, unit: 'MINUTES')
    }
    
    environment {
        AUTHOR = "Aryadi"
        EMAIL = "adiparwira@yahoo.com"
        WEB = "https://chat.openai.com"
    }
    
    parameters {
        string(name: "NAME", defaultValue: "Guest", description: "what is your name")
        text(name: "DESCRIPTION", defaultValue: "Guest", description: "Tell me about you")
        booleanParam(name: "DEPLOY", defaultValue: "false", description: "Need to deloy ?")
        choice(name: "SOCIAL_MEDIA", choices: ['facebook',"instagram","twitter"], description: "which social media")
        password(name: "PASSWORD", defaultValue: "secret", description: "Encrypt key")
    }
    
    
    //triggers {
        //cron("*/2 * * * *")
        //pollSCM("*/5 * * * *")
        //upstream(upstreamProjects: "job1,job2", threshold: hudson.model.Result.SUCCESS )
    //}

    
    stages {
        stage('Parameter') {
            agent {
                node {
                    label "Linux && Java11"
                }
            }
            
            steps {
                echo "Hello ${params.NAME}"
                echo "Your description is ${params.DESCRIPTION}"
                echo "Need to deploy ${params.DEPLOY}"
                echo "Your social media is ${params.SOCIAL_MEDIA}"
                echo "Your secret ${params.PASSWORD}"
            }
        }
        
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
                sh 'echo "APP Password: $APP_PSW" > pass.txt'
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
            input {
                message "Can we delpy ?"
                ok "Yes of course"
                submitter "aryadi,jenkins"
                parameters {
                    choice(name: "TARGET_ENV", choices: ["DEV", "QA", "PROD"], description: "Which Environment ?")
                }
            }
            
            agent {
                node {
                    label "Agent && 2"
                }
            }
            
            steps {
                echo "Deploy to ${TARGET_ENV}"
            }
        
        stage('Release') {
            when {
                expression {
                    return params.DEPLOY
                }
            }
                
            agent {
                node {
                    label "Agent && 2"
                }
            }
            
            steps {
                echo "Release it"
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
