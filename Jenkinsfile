pipeline {
    agent any
    environment {
        CX_VERSION = '2.3.24'
        CX_BASE_URI = 'https://us.ast.checkmarx.net'
        CX_ADDITIONAL_PARAMS = '--scan-types sast,sca,scs'
        CX_PROJECT_NAME = 'cx-devsecops/webgoat'
        
    }
    stages {
        stage('Checkmarx Scan') {
            steps {
                withCredentials([string(credentialsId: 'CX_TENANT', variable: 'CX_TENANT'), string(credentialsId: 'CX_CLIENT_ID', variable: 'CX_CLIENT_ID'), string(credentialsId: 'CX_CLIENT_SECRET', variable: 'CX_CLIENT_SECRET')]) {
                    sh 'mkdir cx-cli; cd cx-cli'
                    sh 'curl -Lo ast-cli.tar.gz https://github.com/Checkmarx/ast-cli/releases/download/${CX_VERSION}/ast-cli_${CX_VERSION}_linux_x64.tar.gz'
                    sh 'tar -xzvf ast-cli.tar.gz'
                    sh './cx scan create -s ${WORKSPACE} --project-name ${CX_PROJECT_NAME} --branch ${GIT_BRANCH} --base-uri ${CX_BASE_URI} --tenant ${CX_TENANT} --client-id ${CX_CLIENT_ID} --client-secret ${CX_CLIENT_SECRET} ${CX_ADDITIONAL_PARAMS}'
                }
            }
        }
    }
    post { 
        always { 
            cleanWs() 
        }
    }
}