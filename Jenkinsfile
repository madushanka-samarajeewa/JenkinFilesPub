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

                echo 'configuring aws cred'
                sh 'aws configure'
                
                withCredentials([string(credentialsId: 'awsaccess', variable: 'SECRET')]) { //set SECRET with the credential content
                
                    << echo $SECRET
                }
                //echo 'accesskey entered'

                withCredentials([string(credentialsId: 'awssecretaccess', variable: 'SECRET')]) { //set SECRET with the credential content
                    
                    echo $SECRET
                }
                //echo 'sec access entered'

                withCredentials([string(credentialsId: 'awsregion', variable: 'SECRET')]) { //set SECRET with the credential content
                
                    echo $SECRET
                }
                //echo 'region entered'

                echo ' '
                
                echo 'Deploying App to s3 bucket'
                sh 'aws s3 sync build/ s3://firstbucketreactapp'
            }
        }
    }
    
}
