// pipeline {
//     agent any 
//     stages {
//         stage('Build') {
//             agent {
//                 docker {
//                     image 'node:18-alpine'
//                     reuseNode true
//                 }
//             }
//             steps {
//                 sh '''
//                 ls -la
//                 node --version
//                 npm --version
//                 npm ci
//                 npm run build
//                 ls -la
//                 '''
//             }
//         }

//         stage('Test') {
//             parallel {
//                 stage('Unit tests') {
//                     agent {
//                         docker {
//                             image 'node:18-alpine'
//                             reuseNode true
//                         }
//                     }
//                     steps {
//                         sh '''
//                         #test -f build/index.html
//                         '''
//                     }
//                 }
//                 stage ('E2E') {
//                     agent {
//                         docker {
//                             image 'mcr.microsoft.com/playwrite:v1.39.0-jammy'
//                             reuseNode true
//                         }
//                     }
//                 }
//             } 
//         } 
//     }

//     post {
//         always {
//             script {
//                 if (fileExists('junit.xml')) {
//                     junit 'junit.xml'

pipeline {
    agent any 
    stages {
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
                npm ci
                npm run build
                ls -la
                '''
            }
        }

        stage('Test') {
            parallel {
                stage('Unit tests') {
                    agent {
                        docker {
                            image 'node:18-alpine'
                            reuseNode true
                        }
                    }
                    steps {
                        sh '''
                        # test -f build/index.html
                        '''
                    }
                }
                stage('E2E') {
                    agent {
                        docker {
                            image 'mcr.microsoft.com/playwright:v1.39.0-jammy'
                            reuseNode true
                        }
                    }
                    steps {
                        echo 'Placeholder for end-to-end test commands'
                    }
                }
            } // <-- closes `parallel`
        } // <-- closes `stage('Test')`
    } // <-- closes `stages`

    post {
        always {
            script {
                if (fileExists('junit.xml')) {
                    junit 'junit.xml'
                } else {
                    echo 'No JUnit test report found. Skipping junit step.'
                }
            }
        }
    }
} 
