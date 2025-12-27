pipeline {
    agent any

    tools {
        maven 'maven' // Nom de l’installation Maven dans Jenkins
    }

    stages {

        stage('Tool Install') {
            steps {
                echo 'Maven installé'
            }
        }

        stage('Clone le dépôt') {
            steps {
                git 'https://github.com/mariahaddouch/Tp32_mariahaddouch.git'
            }
        }

        stage('Build and SonarQube Analysis') {
            parallel {

                stage('Car Service') {
                    steps {
                        bat 'cd car && mvn clean verify sonar:sonar'
                    }
                }

                stage('Client Service') {
                    steps {
                        bat 'cd client && mvn clean verify sonar:sonar'
                    }
                }

                stage('Gateway Service') {
                    steps {
                        bat 'cd gateway && mvn clean package'
                    }
                }
            }
        }

        stage('Docker Compose') {
            steps {
                bat 'docker-compose up -d --build'
            }
        }
    }
}
