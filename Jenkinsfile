pipeline{
    agent any 
    stages{
        stage ("Build") {
            steps{
                sh  'printenv' // imprime les variables d'environement
                
            }
        }
        stage ('Push to ECR'){
            steps{
                script{

                    withEnv (["AWS_ACCESS_KEY_ID=${env.AWS_ACCESS_KEY_ID}", "AWS_SECRET_ACCESS_KEY=${env.AWS_SECRET_ACCESS_KEY}", "AWS_DEFAULT_REGION=${env.AWS_DEFAULT_REGION}"]) {
                        sh 'docker login -u AWS -p (aws ecr-public get-login-password --region us-east-1) public.ecr.aws/h4h9p1u5'
                        sh 'docker build -t app-cicd .'
                        sh 'docker tag app-cicd:latest public.ecr.aws/h4h9p1u5/app-cicd:""$BUILD_ID""'
                        sh 'docker push public.ecr.aws/h4h9p1u5/app-cicd:""$BUILD_ID"" '
                    }
                }
            }
        }
    }
}