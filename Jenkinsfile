pipeline {
    agent any

    tools {
        jdk 'JDK11'        // Your configured JDK in Jenkins
        maven 'Maven3'     // Your configured Maven in Jenkins
    }

    environment {
        TOMCAT_HOME = '/opt/tomcat'  // Your Tomcat installation path
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/ilankumaran1980/Petclinic.git'
            }
        }

        stage('Build') {
            steps {
                dir('spring-petclinic') {       // Change to the folder with pom.xml
                    sh './mvnw clean package -DskipTests'
                }
            }
        }

        stage('Deploy to Tomcat') {
            steps {
                dir('spring-petclinic/target') {
                    sh """
                    cp *.war ${TOMCAT_HOME}/webapps/
                    """
                }
            }
        }
    }

    post {
        success {
            echo "Build & Deployment Successful!"
        }
        failure {
            echo "Build or Deployment Failed. Check logs!"
        }
    }
}
