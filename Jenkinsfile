pipeline
{
    //agent
    agent any
    
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
