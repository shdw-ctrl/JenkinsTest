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
                sh 'javac HelloWorld.java'
                sh '& "C:\\Program Files\\Java\\jdk-22\\bin\\jar.exe" cvf HelloWorld.jar HelloWorld.class'
            }
        }
        stage('Dependency Check') {
            steps {
                dependencyCheck(
                    odcInstallation: 'Default', // Adjust as necessary for your installation
                    failBuildOnCVSS: 7 // Try this if it works
                )
            }
        }
        stage('Publish Dependency Check Report') {
            steps {
                dependencyCheckPublisher pattern: '**/dependency-check-report.xml'
            }
        }
        stage('Code Analysis') {
            steps {
                sh 'sonar-scanner'
            }
        }
    }
}
