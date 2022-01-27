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
    stages {
        stage('injecting creds securely into script') {
            steps {
                sh 'echo ${params.CREDS_PARAMETER}'
            }
        }        
    }
}