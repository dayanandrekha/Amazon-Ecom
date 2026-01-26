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
        dir('Amazon-Web') { // change directory to web module
            sh 'mvn clean package'
            sh 'ls -l target/'
            sh '''
            WAR_FILE=$(ls target/*.war)
            curl --upload-file $WAR_FILE --user admin:admin http://51.120.122.140:8081/manager/text/deploy?path=/Amazon-Ecom
            '''
        }
    }
}

}
