pipeline {
    agent any

    tools {
        maven 'Maven3'
        jdk 'JDK11'
    }

    stages {
        stage('Checkout') {
            steps {
                // Checkout your GitHub repository
                git 'https://github.com/ilankumaran1980/Petclinic.git'
            }
        }

        stage('Build') {
            steps {
                // Navigate into spring-petclinic folder to build
                dir('spring-petclinic') {
                    sh 'mvn clean package -DskipTests'
                }
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying application to Tomcat...'
                sh '''
                sudo systemctl stop tomcat9
                sudo cp spring-petclinic/target/*.jar /var/lib/tomcat9/webapps/petclinic.jar
                sudo systemctl start tomcat9
                '''
            }
        }
    }

    post {
        success {
            echo 'Deployment successful!'
        }
        failure {
            echo 'Build or deployment failed.'
        }
    }
}
