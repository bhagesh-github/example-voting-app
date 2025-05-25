pipeline {
   agent { label 'worker' }
   options { 
        buildDiscarder(logRotator(numToKeepStr: '15'))
        disableConcurrentBuilds()
        retry(2)
        timeout(time: 10, unit: 'MINUTES')
    }
    parameters {
        string(name: 'BRANCH', defaultValue: 'develop', description: '')
        booleanParam(name: 'TEST_CASES', defaultValue: true, description: '')
        choice(name: 'ENV', choices: ['dev', 'qa', 'uat'], description: '')
    }
    stages {
      stage("checkout") {
        steps {
          checkout scm
        }
      }
       stage('Debug') {
            steps {
                sh 'whoami'
                sh 'groups'
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
       stage ("parallel testing"){
            parallel{
                stage("Linux Test"){
                    steps{
                        sh "echo linux"
                        sh "sleep 180"
                    }
                }  
                stage("Windows Test"){
                    steps{
                        sh "echo windows"
                        sh "sleep 180"
                    }
                }                       
        }
    }
    }
}
