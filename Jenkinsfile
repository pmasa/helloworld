pipeline {
 environment {
 registry = "pedromasa/ci"
 registryCredential = 'dockerhub'
 dockerImage = ''
 } 
agent any
 stages {
  stage('Poll') {
   steps{
     checkout scm
    }
   }
  stage('Build & Unit test'){
   steps{
        
        sh 'mvn clean package'
    }
   }
   stage ('Integration Test'){
    steps{
        sh 'mvn clean verify -Dsurefire.skip=true';
     }
   }
  
  stage('Building Docker Image') {
   steps{
     script {
       dockerImage = docker.build registry + ":$BUILD_NUMBER"
     }
  }
 }
 stage('Push Image to Docker Hub ') {
  steps{
    script {
      docker.withRegistry( '', registryCredential ) {
      dockerImage.push()
      dockerImage.push('latest')
   }
  }
 }}
  
   }
}
