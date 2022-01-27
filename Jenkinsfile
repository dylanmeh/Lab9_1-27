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
'com.cloudbees.plugins.credentials.impl.UsernamePasswordCredentialsImpl', defaultValue: '', description: 'Production deployment key', name: 'deployKey', required: true)
    }
    stages {
        stage('injecting creds securely into script') {
            withCredentials([
                usernameColonPassword('credentialsId: 'deployKey', variable: 'DEPLOY_KEY')
            ]) 
            steps {
                sh('curl -u "$DEPLOY_KEY" https://example.com')
            }
        }        
    }
}