// pipeline {
//   agent any
//   stages {
//     stage('Build') {
//       steps {
//         sh 'npm install'
//       }
//     }       
//     // stage('Test') {
//     //   steps {
        
//     //   }
//     // }
//   }
// }


pipeline {  environment {
    registry = "hitheshk/docker-deployment"
    registryCredential = 'dockerhub'
     dockerImage = ''
  }  
  agent any 
   stages {
    stage('Building image') {
      steps{
        script {
          dockerImage = docker.build registry + ":$BUILD_NUMBER"
        }
      }
    }
    stage('Deploy Image') {
    steps{   
       script {
        docker.withRegistry( '', registryCredential ) {
        dockerImage.push()
      }
    }
  }
}
  }
}
