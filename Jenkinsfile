pipeline
{
    //agent
    agent any

    environment{
        ACCESS_KEY=credentials('awsaccess')
        SECRET_ACC_KEY=credentials('awssecretaccess')
        VERSION_NO='1.2'
    }

    parameters {
        string defaultValue: 'dev', description: 'selects which branch of the code should be built', name: 'Branch_Para'
    }
    
    stages{
        stage('Build'){
            steps{

                echo 'go to repo folder and select branch'
                sh """
                    cd /var/jenkins_home/workspace/jenkins-scm-test/
                    git checkout $Branch_Para
                """

                echo 'installing packages'
                sh 'npm install'

                echo 'building the react app'
                sh 'npm run build'
  
            }
        }
        /*

        stage('Passing-AWS0-Credentials'){
            steps{

                 sh """
                    export AWS_ACCESS_KEY_ID=$ACCESS_KEY
                    export AWS_SECRET_ACCESS_KEY=$SECRET_ACC_KEY
                    export AWS_DEFAULT_REGION=us-east-1
                    
                """     
                
            }
        }
        
        */

        stage('Test'){
            steps{
                echo 'Testing the App'
            }
        }

        stage('Artifact-Management'){
            steps{
                echo 'saving the artifact'

                sh """
                    export AWS_ACCESS_KEY_ID=$ACCESS_KEY
                    export AWS_SECRET_ACCESS_KEY=$SECRET_ACC_KEY
                    export AWS_DEFAULT_REGION=us-east-1

                    cd /var/jenkins_home/workspace/jenkins-scm-test/
                    mv build $VERSION_NO

                    zip -r ${VERSION_NO}.zip build

                    aws s3 sync ${VERSION_NO}.zip s3://version-mangement-reactapp

                """

            }
        }

        /*
        stage('Deploy'){
            steps{
                echo 'select build'
                sh 'cd /var/jenkins_home/workspace/jenkins-scm-test'

                echo 'configuring aws cred'
                sh """
                    export AWS_ACCESS_KEY_ID=$ACCESS_KEY
                    export AWS_SECRET_ACCESS_KEY=$SECRET_ACC_KEY
                    export AWS_DEFAULT_REGION=us-east-1

                    echo 'Deploying App to s3 bucket'
                    aws s3 sync build/ s3://firstbucketreactapp 
                    
                """     
                
            }
            
        }
        */
    }
    
}
