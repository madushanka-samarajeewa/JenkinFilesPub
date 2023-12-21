pipeline
{
    //agent
    agent any

    environment{
        ACCESS_KEY=credentials('awsaccess')
        SECRET_ACC_KEY=credentials('awssecretaccess')
    }
    
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
                sh """
                    export AWS_ACCESS_KEY_ID=$ACCESS_KEY
                    export AWS_SECRET_ACCESS_KEY=$SECRET_ACC_KEY
                    export AWS_DEFAULT_REGION=us-east-1
                    aws s3 ls
                    aws s3 sync build/ s3://firstbucketreactapp
                """
                
                echo 'Deploying App to s3 bucket'
                
            }
        }
    }
    
}
