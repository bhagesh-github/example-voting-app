pipeline {
   agent { label 'worker' }
    stages {
      stage("checkout") {
        steps {
          checkout scm
        }
      }
       stage("Docker build and push") {
          steps {
             sh "docker login -u bhageshk -p Bhag@docker00"
             sh '''
                cd vote
                docker build -t bhageshk/vote:v${BUILD_NUMBER} .
                
                '''
             sh "docker push bhageshk/vote:v${BUILD_NUMBER}"
          }
       }
    }
}
