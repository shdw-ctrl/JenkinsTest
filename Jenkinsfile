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
                bat 'javac HelloWorld.java'
                bat '"C:\\Program Files\\Java\\jdk-22\\bin\\jar.exe" cvf HelloWorld.jar HelloWorld.class'
            }
        }
        stage('Dependency Check') {
            steps {
                dependencyCheck additionalArguments: '--scan .', odcInstallation: 'Default'
            }
        }
        stage('Publish Dependency Check Report') {
            steps {
                dependencyCheckPublisher pattern: '**/dependency-check-report.xml'
            }
        }
        stage('Code Analysis') {
            steps {
                bat 'sonar-scanner'
            }
        }
    }
}
