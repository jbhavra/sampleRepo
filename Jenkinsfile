pipeline {
    agent {
        docker {
            image 'node:6-alpine' 
            args '-p 3002:3000' 
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
                sh 'echo test stage' 
            }
        }
    }
}
