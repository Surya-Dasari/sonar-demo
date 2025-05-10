pipeline {
    agent any

    environment {
        SONARQUBE = 'SonarQube'  // This matches the name of your SonarQube server in Jenkins configuration
        GIT_CREDENTIALS = credentials('your-credentials-id')  // Replace with your credentials ID
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'master', url: 'https://github.com/Surya-Dasari/sonar-demo.git', credentialsId: 'your-credentials-id'
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
                    // Execute the SonarQube scanner for the project
                    sh "mvn sonar:sonar -Dsonar.projectKey=sonar-demo -Dsonar.host.url=http://localhost:9000 -Dsonar.login=${SONAR_TOKEN}"
                }
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploy stage goes here'
            }
        }
    }
}
