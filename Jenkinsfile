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
        /* stage('Security Scan') {
              steps { 
                 aquaMicroscanner imageName:'alpine:latest', notCompliesCmd:'exit 1', onDisallowed: 'fail', outputFormat: 'html'
              }
         }         
         stage('Upload to AWS') {
              steps {
                   withAWS(region: 'us-east-2', credentials: 'devopsroot') {
                        sh 'echo "Uploading content with AWS creds"'
                        s3Upload(pathStyleAccessEnabled: true, excludePathPattern : '*Jenkins*', includePathPattern : '*.html, css/*, img/*, vendor/**, __MACOSX/**', bucket: 'batram-static-pipeline')
                  }
              }
         }*/
     }
}