pipeline {
    agent any

    tools {
        maven 'Maven'
    }

    stages {

        stage('CompileandRunSonarAnalysis') {
            steps {
                sh '''
                mvn clean verify sonar:sonar \
                -Dsonar.projectKey=secguru123 \
                -Dsonar.organization=secguru123 \
                -Dsonar.host.url=https://sonarcloud.io \
                -Dsonar.token=958058fac36d22a25096e9ae5a285c04298bdcdf
                '''
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
