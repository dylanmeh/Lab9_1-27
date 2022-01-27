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
        credentials(
            credentialType: 'com.cloudbees.plugins.credentials.impl.UsernamePasswordCredentialsImpl',
            defaultValue: '',
            description: 'The crednetials needed to deploy'
            name: 'deployCredentialsId',
            required: true
        )
    }
    stages {
        stage('injecting creds as build time parameter') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: '${deployCredentialsId}',
                    usernameVariable: 'DEPLOY_USERNAME',
                    passwordVariable: 'DEPLOY_PASSWORD',
                )]) {
                    sh 'echo "${DEPLOY_USERNAME}"'
                }
            }
        }        
    }
}