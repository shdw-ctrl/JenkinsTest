pipeline {
    agent any
    stages {
        stage('Clone') {
            steps {
                git 'https://github.com/carwoof444/jenkinstest'
            }
        }
        stage('Build') {
            steps {
                sh 'javac HelloWorld.java'
            }
        }
        stage('Security Scan') {
            steps {
                sh 'java HelloWorld'
            }
        }
    }
}
