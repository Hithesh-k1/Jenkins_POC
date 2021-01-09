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

// pipeline {
//     environment {
//         registry = 'hitheshk/docker-deployment'
//         registryCredential = 'dockerhub'
//         dockerImage = ''
//     }
//     agent any
//     stages {
//         stage('Building image') {
//             steps {
//                 script {
//                     dockerImage = docker.build registry + ":$BUILD_NUMBER"
//                 }
//             }
//         }
//         stage('Deploy Image') {
//             steps {
//                 script {
//                     docker.withRegistry( '', registryCredential )
//                     {
//                         dockerImage.push()
//                     }
//                 }
//             }
//         }
//     }
// }

// pipeline {
//     agent any
//     stages {
//         stage('Build') {
//             steps {
//                 echo 'Building..'
//             }
//         }
//         stage('Test') {
//             steps {
//                 echo 'Testing..'
//             }
//         }
//         stage('Deploy') {
//             steps {
//                 echo 'Deploying....'
//             }
//         }
//     }
// }


pipeline {
    agent any
    stages {
        stage('SCM') {
            steps {
                git url: 'https://github.com/Hithesh-k1/Jenkins_POC.git'
            }
        }
        stage('build && SonarQube analysis') {
            steps {
                withSonarQubeEnv('My SonarQube Server') {
                    // Optionally use a Maven environment you've configured already
                    withMaven(maven:'Maven 3.5') {
                        sh 'mvn clean package sonar:sonar'
                    }
                }
            }
        }
        stage('Quality Gate') {
            steps {
                timeout(time: 1, unit: 'HOURS') {
                    // Parameter indicates whether to set pipeline to UNSTABLE if Quality Gate fails
                    // true = set pipeline to UNSTABLE, false = don't
                    waitForQualityGate abortPipeline: true
                }
            }
        }
    }
}