pipeline {
    agent any

    environment {
        PATH = "/opt/maven/bin:$PATH"
    }

    stages {
        stage('Build') {
            steps {
                echo '------------Building----------------'
                sh 'mvn clean deploy -Dmaven.test.skip=true'
                echo '--------------Build completed------------'
            }
        }

        stage('Testing') {
            steps {
                echo '-------Testing in progress----------'
                sh 'mvn surefire-report:report'
                echo '------Testing completed--------------'
            }
        }

        stage('Sonarqube testing') {
            environment {
                scannerHome = tool 'project44-sonar-scanner'
            }
            steps {
                withSonarQubeEnv('project44-sonar-server') {
                    sh "${scannerHome}/bin/sonar-scanner"
                }
            }
        }
    }
}

