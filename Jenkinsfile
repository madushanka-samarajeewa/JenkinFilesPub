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

                // echo 'go to repo folder and select branch'
                // sh """
                //     cd /var/jenkins_home/workspace/jenkins-scm-test/
                //     git checkout $Branch_Para
                // """

                // echo 'installing packages'
                // sh 'npm install'

                // echo 'building the react app'
                // sh 'npm run build'
  
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
                script{

                
                /*
                echo 'aquiring the latest version'

                vArray=(0 6 10 2)
                max_version=0
                for tempVer in ${vArray[@]}; do
                if [ $max_version -lt $tempVer ];
                then
                    max_version=$tempVer
                fi
                done
                echo max version is : ${max_version}
                

                */
                
                   
                
                echo 'aquiring the latest version'
                LATEST_VERSION = versioning($ACCESS_KEY, $SECRET_ACC_KEY)
                echo "latest version $LATEST_VERSION"
                /*
                sh '''

                    export AWS_ACCESS_KEY_ID=$ACCESS_KEY
                    export AWS_SECRET_ACCESS_KEY=$SECRET_ACC_KEY
                    export AWS_DEFAULT_REGION=us-east-1
                    
                    vArray=(`aws s3 ls s3://version-mangement-reactapp/ | awk '{print $4}' | sort -V`)
                    max_version=${vArray[-1]}
                    max_version=${max_version%.zip}
                   
                    echo "max version is : ${max_version}"

                    IFS='.' read -ra ADDR <<< "$max_version"
                    ADDR[1]=$((ADDR[1]+1))
                    new_version="${ADDR[0]}.${ADDR[1]}"
                    echo "max version is : $new_version"

                    VERSION_NO=$new_version
                    echo "new application version is : ${VERSION_NO}"

                '''
                */

                /*
                sh"""
                    export AWS_ACCESS_KEY_ID=$ACCESS_KEY
                    export AWS_SECRET_ACCESS_KEY=$SECRET_ACC_KEY
                    export AWS_DEFAULT_REGION=us-east-1
                """
                script {

                    def max_version = sh(script: "aws s3 ls s3://version-mangement-reactapp/ | awk '{print \$4}' | sort -V | tail -n1", returnStdout: true).trim()
                    max_version = max_version.minus(".zip")
                    echo "max version is : ${max_version}"

                    def (major, minor) = max_version.tokenize('.')
                    minor = minor.toInteger() + 1
                    def new_version = "${major}.${minor}"
                    echo "new version is : ${new_version}"

                    VERSION_NO=${new_version}

                }
                */

                /*
                echo 'saving the artifact'

                sh """
                    export AWS_ACCESS_KEY_ID=$ACCESS_KEY
                    export AWS_SECRET_ACCESS_KEY=$SECRET_ACC_KEY
                    export AWS_DEFAULT_REGION=us-east-1

                    cd /var/jenkins_home/workspace/jenkins-scm-test/

                    zip -r ${VERSION_NO}.zip build

                    aws s3 cp ${VERSION_NO}.zip s3://version-mangement-reactapp

                """
                */
                }
            }
        }

        /*
        stage('Deploy'){
            steps{
                echo 'select build'
                sh """ 
                    cd /var/jenkins_home/workspace/jenkins-scm-test
                    mkdir tempDown
                    cd tempDown

                    echo 'configuring aws cred'
                    export AWS_ACCESS_KEY_ID=$ACCESS_KEY
                    export AWS_SECRET_ACCESS_KEY=$SECRET_ACC_KEY
                    export AWS_DEFAULT_REGION=us-east-1

                    echo 'Downloading the latest version of the application'
                    aws s3 cp s3://version-mangement-reactapp/${VERSION_NO}.zip .
                    unzip ${VERSION_NO}.zip


                    echo 'Deploying App to s3 bucket'
                    aws s3 sync build/ s3://firstbucketreactapp 
                    
                """    
                
            }
            
        }
        */
        
    }
    
}
def versioning(ACCESS_KEY,SECRET_ACC_KEY)
{
    writeFile file:'test.sh', text: '''#!/bin/bash
        echo "access key $1"
        export AWS_ACCESS_KEY_ID=$1
        export AWS_SECRET_ACCESS_KEY=$2
        export AWS_DEFAULT_REGION=us-east-1

        vArray=(`aws s3 ls s3://version-mangement-reactapp/ | awk '{print \$4}' | sort -V`)
        max_version=${vArray[-1]}
        max_version=${max_version%.zip}
        echo "max version is : ${max_version}"

        IFS='.' read -ra ADDR <<< "$max_version"
        ADDR[1]=$((ADDR[1]+1))
        new_version="${ADDR[0]}.${ADDR[1]}"
        echo $new_version
    '''

    new_version = sh (
    script: "chmod +x test.sh && ./test.sh",
    returnStdout: true
    ).trim()
    sh "rm -f test.sh"
    return new_version
}
