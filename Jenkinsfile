properties([
    podTemplate(containers: [
    containerTemplate(name: 'maven', image: 'maven:3.8.1-jdk-11', command: 'sleep', args: '99d')
]) {
    parameters([
        credentials(credentialType:
'com.cloudbees.plugins.credentials.impl.UsernamePasswordCredentialsImpl', defaultValue: '', description: 'Production deployment key', name: 'deployKey', required: true)
    ])
    node(POD_LABEL) {
        stage('injecting creds securely into script') {
            withCredentials([usernameColonPassword('credentialsId: 'deployKey', variable: 'DEPLOY_KEY')]) {
                sh('curl -u "$DEPLOY_KEY" https://example.com')
            }
        }        
    }
}