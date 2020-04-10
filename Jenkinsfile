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
            when{
                expression {
                    env.BRANCH_NAME == "master"
                }
            }
            steps{
                input message: 'Proceed for dev deployment?'
            }
        }

        stage('Deploy-Dev'){
            when{
                expression {
                    env.BRANCH_NAME == "master"
                }
            }
            steps{
                sh '''
                    set -x
                    npm run build
                    set +x

                    set -x
                    npm start &
                    sleep 1
                    echo $! > .pidfile
                    set +x
                    
                  '''
            }
        }

        stage('finish'){
            when{
                expression {
                    env.BRANCH_NAME == "master"
                }
            }
            steps{
                input message: 'Stop App?'
            }
        }

        stage ('stop app'){
            when{
                expression {
                    env.BRANCH_NAME == "master"
                }
            }
            steps{
                sh '''
                    set -x
                    kill $(cat .pidfile)
                   '''
            }
        }
    }
}
