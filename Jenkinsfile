//author: Subhadeep dasgupta
pipeline {
  environment{
    registry = "deepdasgupta231182/pipeline_repo82"
    registryCredential = '25d7b971-2c9e-4657-a683-2656cc8ffc13'
    dockerImage = ''
    containerId = sh(script: 'docker ps -aqf "name=node-app"', returnStdout:true)
  }
  agent any
  tools {nodejs "node"}
    
  stages {
    stage('Cloning Git') {
      steps {
        git 'https://github.com/subhadeepdasgupta1982/node-todo-frontend'
      }
    }
        
    stage('Build') {
      steps {
        sh 'npm install'
      }
    }
     
    stage('Test') {
      steps {
         sh 'npm test'
      }
    }
    stage('Building Image'){
      steps{
        script{
          dockerImage = docker.build registry + ":$BUILD_NUMBER"
        }
        stage('Push Image'){
      steps{
        script{
          docker.withRegistry('',registryCredential) {
            dockerImage.push()
          }
        }
      }
        }
      }
    }
  }
}
    
