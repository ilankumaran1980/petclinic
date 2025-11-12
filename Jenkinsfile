pipeline {
    agent any

    tools {
        maven 'Maven3'   // Matches Maven installation name in Jenkins
        jdk 'JDK11'      // Matches JDK name in Jenkins
    }

    environment {
        TOMCAT_HOME = "/usr/share/tomcat9"  // Tomcat installation path
        APP_NAME = "petclinic"              // App folder name in Tomcat webapps
    }

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/ilankumaran1980/Petclinic.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package -DskipTests' // build jar/war
            }
        }

        stage('Deploy to Tomcat') {
            steps {
                // Copy WAR to Tomcat webapps
                sh '''
                cp target/*.war $TOMCAT_HOME/webapps/$APP_NAME.war
                sudo systemctl restart tomcat9
                '''
            }
        }
    }

    post {
        success {
            echo 'Deployment completed successfully!'
        }
        failure {
            echo 'Deployment failed. Check logs!'
        }
    }
}
