pipeline {
     agent any
     stages {
          stage('Build') {
            steps {
                sh 'echo "Hello World"'
                sh '''
                    echo "Multiline shell steps works too"
                    ls -lah
                    '''
              }
         }
            stage('Tidy Check') {
            steps {
                sh 'tidy -q -e jenkins_pipeline/index.html'
              }
         }
            stage('Upload to AWS') {
                steps {
                    withAWS(region:'eu-north-1',credentials:'AWS_access') {
                    sh 'echo "Uploading content with AWS creds"'
                        s3Upload(pathStyleAccessEnabled: true, payloadSigningEnabled: true, file:'jenkins_pipeline/index.html', bucket:'jenkins-11987')
                    }
                }
            }
     }
}