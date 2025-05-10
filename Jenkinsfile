pipeline {
    agent any

    tools {
        maven 'Maven 3.8.1'
    }

    environment {
        SONARQUBE_URL = 'http://localhost:9000'  // URL of SonarQube server
        SONAR_TOKEN = credentials('jenkins-token')  // This is the credentials ID for the SonarQube token stored in Jenkins
    }

    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/Surya-Dasari/sonar-demo.git', branch: 'master', credentialsId: 'github-pat'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean install'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                script {
                    // Run SonarQube analysis using Maven's sonar plugin
                    sh "mvn sonar:sonar -Dsonar.projectKey=sonar-demo -Dsonar.host.url=${SONARQUBE_URL} -Dsonar.login=${SONAR_TOKEN}"
                }
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploy stage goes here'
            }
        }

        stage('Archive') {
            steps {
                archiveArtifacts artifacts: '**/target/*.jar', fingerprint: true
            }
        }
    }
}
