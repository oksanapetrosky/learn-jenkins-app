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
            stage ('Test') {
                agent {
                docker {
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps {
                sh '''
                test -f build/index.html
                '''
          }
        }    
    }
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