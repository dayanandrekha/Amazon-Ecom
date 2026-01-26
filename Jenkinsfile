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
   
   stage('clone project') {
      steps {
           git branch:'master' , url:'https://github.com/dayanandrekha/Amazon-Ecom.git'
       }
   }

   stage('clean') {
      steps {
           sh 'mvn clean'
       }
   }

   stage('compile') {
      steps {
           sh 'mvn compile'
       }
   }

   stage('test') {
      steps {
           sh 'mvn test'
       }
   }

   stage('build') {
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
                ${TOMCAT_URL}/deploy?path=/${APP_NAME}&update=true
                """
            }
        }
    }
}
   
}

}
