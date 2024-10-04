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
                        /opt/sonar-scanner/bin/sonar-scanner \
                        -Dsonar.projectKey=Sparta-pipeline \  // Change this to your desired project key
                        -Dsonar.sources=. \
                        -Dsonar.java.binaries=./ \  // Specifies the location of compiled classes
                        -Dsonar.dependencyCheck.reportPath=dependency-check-report.xml \
                        -Dsonar.host.url=http://localhost:9000 \
                        -Dsonar.login=sqp_6af7202a9982ccecb9a0faa8176e5594f29a751e  // Your SonarQube token
                    '''
                }
            }
        }
    }
}

