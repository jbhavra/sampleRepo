pipeline {
    agent {
        docker {
            image 'node:6-alpine'
        }
    }

    environment {
        CI = 'true'
    }

    stages {
        stage('Build') { 
            steps {
                sh 'npm install' 
            }
        }

        stage('Test'){
            steps{
                sh 'npm test'
            }
        }

        stage('Promote To Dev'){
            steps{
                input message: 'Proceed for dev deployment?'
            }
        }

        stage('Deploy-Dev'){
            steps{
                sh '''
                    set -x
                    npm run build
                    set +x

                    set -x
                    npm start &
                    sleep 1
                    echo $!
                    set +x
                    
                  '''
            }
        }
    }
}
