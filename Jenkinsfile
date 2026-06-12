pipeline {
    agent any

    tools {
        maven 'Maven'
    }

    stages {

        stage('Build') {
            steps {
                 sh 'mvn clean verify sonar:sonar -Dsonar.projectKey=mdmaaz-superagent -Dsonar.organization=mdmaaz-superagent -Dsonar.host.url=https://app.snyk.io/org/mdmaaz-superagent -Dsonar.token=9f1e40a6-e3ed-4355-ab8c-3179e8927fab'
            }
        }

        stage('Snyk SCA Scan') {
            steps {
                withCredentials([string(credentialsId: 'SNYK_TOKEN', variable: 'SNYK_TOKEN')]) {
                    sh '''
                        snyk auth $SNYK_TOKEN
                        snyk test
                    '''
                }
            }
        }
    }
}
