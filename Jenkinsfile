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

// pipeline {
//     agent any
//     stages {
//         stage('SCM') {
//             steps {
//                 git url: 'https://github.com/Hithesh-k1/Jenkins_POC.git'
//             }
//         }
//             stage('Build') {
//             steps {
//                 echo 'Building...'
//                 sh ' npm install'
//                 sh ' npm run build'
//             }
//             }
//         stage('Test') {
//             steps {
//                 echo 'Testing..'
//             }
//         }
        // stage('Sonarqube') {
        //     environment {
        //         scannerHome = tool 'SonarQubeScanner'
        //     }
        //     steps {
        //         withSonarQubeEnv('sonarqube') {
        //             sh "${scannerHome}/bin/sonar-scanner"
        //         }
        //         timeout(time: 10, unit: 'MINUTES') {
        //             waitForQualityGate abortPipeline: true
        //         }
        //     }
        // }

        // stage('Sonarqube analysis') {
        //     steps {
        //         script {
        //             scannerHome = tool 'SonarScanner'
        //         }
        //         withSonarQubeEnv('SonarQube') {
        //             sh "${scannerHome}/bin/sonar-scanner.sh"
        //         }
        //     }
        // }

        // stage('build && SonarQube analysis') {
        //     steps {
        //         withSonarQubeEnv('My SonarQube Server') {
        //             // Optionally use a Maven environment you've configured already
        //             withMaven(maven:'Maven 3.5') {
        //                 sh 'mvn clean package sonar:sonar'
        //             }
        //         }
        //     }
        // }
        // stage('Quality Gate') {
        //     steps {
        //         timeout(time: 1, unit: 'HOURS') {
        //             // Parameter indicates whether to set pipeline to UNSTABLE if Quality Gate fails
        //             // true = set pipeline to UNSTABLE, false = don't
        //             waitForQualityGate abortPipeline: true
        //         }
        //     }
        // }

    // stage('Quality Gate') {
    //     steps {
    //         timeout(time: 1, unit: 'HOURS') {
    //             // Parameter indicates whether to set pipeline to UNSTABLE if Quality Gate fails
    //             // true = set pipeline to UNSTABLE, false = don't
    //             waitForQualityGate abortPipeline: true
    //         }
    //     }
    // }
//     }
// }


pipeline {
    agent any
       stages {
        stage('Install') {
            steps {
                echo 'Installation...'
                sh 'npm install'
            }
        }
        stage('Test') {
            steps {
                echo 'Testing...'
                sh 'npm test'
            }
        }
        stage('Sonarqube') {
            environment {
                 scannerHome = tool 'sonar_scanner'
            }
            
            steps {
                echo 'Scanning....'
                withSonarQubeEnv('SonarQube') {
                sh "${scannerHome}/bin/sonar-scanner"
             }
                timeout(time: 10, unit: 'MINUTES') {
                waitForQualityGate abortPipeline: true
            }
        }
    }
    stage('Build') {
            steps {
                echo 'Production build...'
                sh 'npm run build'
            }
        }
    }
}