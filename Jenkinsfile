// pipeline {
//     agent any

//     stages {
//         stage('Clean'){
//             steps{
//                 cleanWs();
//             }
//         }
//         stage('Build') {
//             agent {
//                 docker {
//                     image 'node:18-alpine'
//                     reuseNode true
//                 }
//             }
//             steps {
//                 sh '''
//                     ls -la
//                     node --version
//                     npm --version
//                     npm ci
//                     npm run build
//                     ls -la
//                 '''
//             }
//         }
//         stage('Test') {
//             steps {
//                 sh '''
//                     test -f build/index.html
//                 '''
//             }
//         }


//     }
// }
pipeline {
    agent any

    options {
        skipDefaultCheckout(true)
    }

    stages {
        stage('Pre-Clean') {
            steps {
                cleanWs()
            }
        }

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            agent {
                docker {
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps {
                sh '''
                    ls -la
                    node --version
                    npm --version
                    npm install
                    npm run build
                    ls -la
                '''
            }
        }

        stage('Test') {
            steps {
                sh 'test -f build/index.html'
            }
        }
    }
}

