pipeline {
    agent any

    stages{
        stage ("getting-aws-creds ") {
            steps {
               withCredentials([[
        $class: 'AmazonWebServicesCredentialsBinding',
        credentialsId: 'shitalkumar-aws	',
        accessKeyVariable: 'AWS_ACCESS_KEY_ID',
        secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']])
            }
        }
    
        stage('Checkout') {
            steps {
                checkout scmGit(branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/shitalkumar58627/myInfra-aws-2022Repo.git']])
            }
        }

         stage ("terraform init") {
            steps {
                sh ("terraform init -reconfigure") 
            }
        }

        stage ("plan") {
            steps {
                sh ('terraform plan') 
            }
        }


stage (" Action") {
            steps {
                echo "Terraform action is --> ${action}"
                sh ('terraform ${action} --auto-approve') 
           }
        }

  }
}







    
