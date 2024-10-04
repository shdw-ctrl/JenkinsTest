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
        stage('Code Analysis') {
            steps {
                withSonarQubeEnv('SonarQube') {  // 'SonarQube' is the name of your server setup in Jenkins
                    sh '''
                        /opt/sonar-scanner/bin/sonar-scanner -Dsonar.projectKey='Sparta-pipeline' -Dsonar.sources=. -Dsonar.java.binaries=./ -Dsonar.dependencyCheck.reportPath=dependency-check-report.xml -Dsonar.host.url=http://localhost:9000 -Dsonar.login=sqa_a00257ae7497505be00e567cbccdbe78882b4009 
                    '''
                }
            }
        }
    }
}

