pipeline {
    agent any
    environment {
        CX_VERSION = '2.3.24'
        CX_BASE_URI = 'htpps://ast.checkmarx.net'
        CX_TENANT = 'ferreiralucas-sedemo'
        CX_CLIENT_ID = 'jenkins-plugin'
        CX_CLIENT_SECRET = 'htYnAde9Ku9xIJRO8lYZPJrw2z2LzE8J'
        CX_ADDITIONAL_PARAMS = ''
    }
    stages {
        stage('Checkmarx Scan') {
            steps {
                sh 'echo ### Download Cx CLI ###'
                sh 'mkdir cx-ast; cd cx-ast'
                sh 'curl -Lo ast-cli.tar.gz https://github.com/Checkmarx/ast-cli/releases/download/${CX_VERSION}/ast-cli_${CX_VERSION}_linux_x64.tar.gz'
                sh 'tar -xzvf ast-cli.tar.gz'
                sh './cx'
            }
        }
    }
}