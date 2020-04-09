pipeline {
    agent {
        docker {
            image 'node:6-alpine' 
        }
    }
    stages {
        stage('Build') { 
            steps {
                sh 'npm install' 
            }
        }
        
        stage('Test') { 
            steps {
                echo 'test stage' 
            }
        }
        
        stage('Dev') { 
            steps {
                echo 'dev stage' 
            }
        }
    }
}
