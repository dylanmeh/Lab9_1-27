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
    parameters {
        credentials(credentialType:
'com.cloudbees.plugins.credentials.impl.UsernamePasswordCredentialsImpl'
                    defaultValue: '',
                    description: 'Production deployment key',
                    name: 'deployKey',
                    required: true)
    }
    stages {
        stage('injecting creds securely into script') {
            environment {
                DEPLOY_KEY = usernameColonPassword('deployKey')
            }
            steps {
                sh 'echo "$DEPLOY_KEY"'
            }
        }        
    }
}