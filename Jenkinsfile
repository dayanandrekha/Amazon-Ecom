pipeline {
    agent any

    environment {
        TOMCAT_URL = 'http://51.120.122.140:8081/manager/text'
        TOMCAT_USER = 'admin'
        TOMCAT_PASSWORD = 'admin'
        APP_NAME = 'Amazon-Ecom'
    }

    stages {

        stage('Clone Project') {
            steps {
                git branch: 'master', url: 'https://github.com/dayanandrekha/Amazon-Ecom.git'
            }
        }

        stage('Clean') {
            steps {
                dir('Amazon-Ecom/Amazon-Web') {
                    sh 'mvn clean'
                }
            }
        }

        stage('Compile') {
            steps {
                dir('Amazon-Ecom/Amazon-Web') {
                    sh 'mvn compile'
                }
            }
        }

        stage('Test') {
            steps {
                dir('Amazon-Ecom/Amazon-Web') {
                    sh 'mvn test'
                }
            }
        }

        stage('Build') {
            steps {
                dir('Amazon-Ecom/Amazon-Web') {
                    sh 'mvn clean install'
                }
            }
        }

        stage('Deploy to Tomcat') {
            steps {
                dir('Amazon-Ecom/Amazon-Web') {
                    echo "Deploying WAR to Tomcat..."
                    sh """
                    curl --upload-file target/Amazon.war \
                    --user ${TOMCAT_USER}:${TOMCAT_PASSWORD} \
                    ${TOMCAT_URL}/deploy?path=/${APP_NAME}&update=true
                    """
                }
            }
        }
    }
}
