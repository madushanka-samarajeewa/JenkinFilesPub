pipeline
{
    //agent any
    agent {
        docker {
            image 'node:20.10.0-alpine3.19' 
            args '-p 3200:3000' 
        }
    
    stages{
        stage('Build'){
            steps{
                sh 'npm install'
                echo 'Build App'
                
            }
        }

        stage('Test'){
            steps{
                echo 'Test App'
            }
        }

        stage('Deploy'){
            steps{
                echo 'Deploy App'
            }
        }
    }
    
}
