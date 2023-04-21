pipeline {
    agent any

    tools {
        maven 'Maven'
    }

    stages {
        stage('Build') {
            steps {
                sh 'mvn clean install'
            }
        }

        stage('SonarQube analysis') {
            steps {
                withSonarQubeEnv('SonarQube') {
                    sh 'mvn sonar:sonar'
                }
            }
        }

        stage('Run') {
            steps {
                sh 'java -Dserver.port=9090 -jar target/*.jar &'
                echo 'PetClinic application started'
            }
        }
    }
}
