pipeline{
    agent any 
    stages{
        // stage ("Build") {
        //     steps{
        //         bat  'printenv' // imprime les variables d'environement
                
        //     }
        // }
        stage ('Push to ECR'){
            steps{
                script{

                    withEnv (["AWS_ACCESS_KEY_ID=${env.AWS_ACCESS_KEY_ID}", "AWS_SECRET_ACCESS_KEY=${env.AWS_SECRET_ACCESS_KEY}", "AWS_DEFAULT_REGION=${env.AWS_DEFAULT_REGION}"]) {
                        bat '''
                            aws ecr-public get-login-password --region us-east-1 | docker login --username AWS --password-stdin public.ecr.aws/h4h9p1u5
                        '''
                        bat '''
                            docker build -t app-cicd .
                        '''
                        bat ''' 
                            docker tag app-cicd:latest public.ecr.aws/h4h9p1u5/app-cicd:""$BUILD_ID""
                        '''
                        bat ''' 
                            docker push public.ecr.aws/h4h9p1u5/app-cicd:""$BUILD_ID"" 
                        '''
                    }
                }
            }
        }
    }
}