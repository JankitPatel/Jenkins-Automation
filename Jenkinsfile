pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                script {
                    docker.image('maven:3.9.0').inside('-v /c/data/jenkins_home/workspace/Maven app pipeline:/workspace') {
                        bat 'mvn -B -DskipTests clean package'
                    }
                }
            }
        }
        stage('Test') {
            steps {
                script {
                    docker.image('maven:3.9.0').inside('-v /c/data/jenkins_home/workspace/Maven app pipeline:/workspace') {
                        bat 'mvn test'
                    }
                }
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }
        stage('Deliver') {
            steps {
                script {
                    bat './jenkins/scripts/deliver.bat'
                }
            }
        }
    }
}
