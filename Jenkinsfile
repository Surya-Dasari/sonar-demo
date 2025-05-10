pipeline {
    agent any

    tools {
        maven 'Maven 3.8.1'
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
                    sh "mvn sonar:sonar -Dsonar.projectKey=sonar-demo -Dsonar.host.url=http://localhost:9000"
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
