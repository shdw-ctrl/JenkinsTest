pipeline {
    agent any
    stages {
        stage('Clone') {
            steps {
                git 'https://github.com/carwoof444/JenkinsTest'
            }
        }
        stage('Build') {
            steps {
                sh './build.sh' // For Java: mvn clean package
            }
        }
        stage('Security Scan') {
            steps {
                sh 'dependency-check --scan ./ --out report'
            }
        }
    }
}
