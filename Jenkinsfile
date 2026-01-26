pipeline {
    agent any

    environment {
        TOMCAT_URL = 'http://51.120.122.140:8080/manager/text'
        TOMCAT_USER = 'admin'
        TOMCAT_PASSWORD = 'admin'
        WAR_FILE = 'target/Amazon-Ecom.war'
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
                sh 'mvn clean'
            }
        }

        stage('Compile') {
            steps {
                sh 'mvn compile'
            }
        }

        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean install'
            }
        }

        stage('Deploy to Tomcat') {
            steps {
                echo "Deploying WAR to Tomcat..."
                sh """
                curl --upload-file ${WAR_FILE} \
                --user ${TOMCAT_USER}:${TOMCAT_PASSWORD} \
                ${TOMCAT_URL}/deploy_
