pipeline
{
    //agent
    agent {
        docker {
            image 'node:20.10.0-alpine3.19' 
            args '-p 3000:3000' 
        }
    }
    
    stages{
        stage('Build'){
            steps{

                echo 'Build App-before npm install'
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
