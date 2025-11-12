pipeline {
    agent any

    tools {
        maven 'Maven3'   // Must match Maven name in Jenkins
        jdk 'JDK11'      // Must match JDK name in Jenkins
    }

   environment {
    PATH = "/opt/maven/bin:${env.PATH}"   // Maven path
    TOMCAT_HOME = "/opt/tomcat"          // Tomcat path
    APP_NAME = "petclinic"
}

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/ilankumaran1980/Petclinic.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package -DskipTests'
            }
        }

      stage('Deploy to Tomcat') {
    steps {
        sh '''
        cp target/*.war $TOMCAT_HOME/webapps/$APP_NAME.war
        systemctl restart tomcat.service
        '''
    }
}
    }

    post {
        success { echo 'Deployment completed successfully!' }
        failure { echo 'Deployment failed. Check logs!' }
    }
}
