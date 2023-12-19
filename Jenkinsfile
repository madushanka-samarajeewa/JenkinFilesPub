pipeline
{
    //agent
    agent any
    
    stages{
        stage('Build'){
            steps{

                echo 'go to repo folder'
                sh 'cd /var/jenkins_home/workspace/jenkins-scm-test/'

                echo 'installing packages'
                sh 'npm install'

                echo 'building the react app'
                sh 'npm run build'
  
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
