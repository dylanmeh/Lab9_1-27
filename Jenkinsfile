pipeline {
    agent {
        kubernetes {
            yaml '''
apiVersion: v1
kind: Pod
spec:
  containers:
  - name: build
    image: 'maven:3.8.3-jdk-11'
    command:
    - cat
    tty: true
    '''
        defaultContainer 'build'
        }
    }
    environment {
        CREDS = credentials('creds-id')
    }
    stages {
        stage('injecting creds securely into script') {
            steps {
                sh("curl -u ${CREDS_USR}:${CREDS_PSW} https://example.com")
            }
        }        
    }
}