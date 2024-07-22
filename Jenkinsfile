pipeline {
    agent any
    stages {
        stage('OWASP Dependency-Check Vulnerabilities') {
            steps {
                withCredentials([string(credentialsId: 'nvd-api-key', variable: 'NVD_API_KEY')]) {
                    dependencyCheck additionalArguments: '''
                        -o './'
                        -s './'
                        -f 'ALL'
                        --prettyPrint
                        --nvdApiKey '${NVD_API_KEY}'
                    ''', odcInstallation: 'OWASP Dependency-Check Vulnerabilities'
                    
                    dependencyCheckPublisher pattern: 'dependency-check-report.xml'
                }
            }
        }
    }    
    post {
        success {
            dependencyCheckPublisher pattern: 'dependency-check-report.xml'
        }
    }
}
