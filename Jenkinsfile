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
                echo 'Testing the App'
            }
        }

        stage('Deploy'){
            steps{
                echo 'select build'
                sh 'cd /var/jenkins_home/workspace/jenkins-scm-test'

                echo 'extrating the region'
                withCredentials([string(credentialsId: 'testregion', variable: 'SECRET')]) { //set SECRET with the credential content
                echo "My secret text is '${SECRET}'"
                echo "My secret text is $SECRET"
                }

                
                echo 'Deploying App to s3 bucket'
                sh 'aws s3 sync build/ s3://firstbucketreactapp'
            }
        }
    }
    
}
