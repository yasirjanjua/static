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
          stage('Lint HTML') {
               steps {
                    sh 'tidy -q -e *.html'
               }
          }
         stage('Upload to AWS') {
             steps {
                 withAWS(region:'us-east-1',credentials:'aws-static') {
                 sh 'echo "Uploading content with AWS creds"'
                    s3Upload(pathStyleAccessEnabled: true, payloadSigningEnabled: true, file:'index.html', bucket:'udacity-jenkins-bucket')
                 }
             }
         }
         stage('Ensure Content') {
               steps {
                  sh  'curl https://udacity-jenkins-bucket.s3.amazonaws.com/index.html'
               }
         }
    }
}
