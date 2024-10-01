pipeline {
    agent any
    stages {
        stage('Clone') {
            steps {
                git branch: 'main', url: 'https://github.com/carwoof444/jenkinstest'
            }
        }
        stage('Build') {
            steps {
                // Compile the HelloWorld.java file
                sh 'javac HelloWorld.java'
            }
        }
        stage('Run') {
            steps {
                // Run the compiled Java class
                sh 'java HelloWorld'
            }
        }
        stage('Dependency Check') {
            steps {
                // Run OWASP Dependency Check analysis
                dependencyCheck('**/*.jar') // Adjust the pattern if necessary
            }
        }
        stage('Publish Dependency Check Report') {
            steps {
                // Publish the Dependency Check report
                dependencyCheckPublisher pattern: '**/dependency-check-report.xml'
            }
        }
        stage('Code Analysis') {
            steps {
                // Run SonarQube analysis
                sh 'sonar-scanner' // Ensure sonar-scanner is installed and configured
            }
        }
    }
}
