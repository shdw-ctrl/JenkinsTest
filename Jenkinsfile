pipeline {
    agent any
    stages {
        stage('Clone') {
            steps {
                git branch: 'main', url: 'https://github.com/carwoof444/JenkinsTest'
            }
        }
        stage('Build') {
            steps {
                sh 'javac HelloWorld.java'
                sh 'jar cvf HelloWorld.jar HelloWorld.class'
            }
        }
        stage('Dependency Check') {
            steps {
                dependencyCheck additionalArguments: '', odcInstallation: 'OWASP-DC'
                dependencyCheckPublisher pattern: 'dependency-check-report.xml'
            }
        }
    }
}
