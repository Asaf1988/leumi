pipline {
    agent none
    enviroment {

    }

    stages {
        agent {label 'agent1'}
        steps{
            sh 'sudo docker build -t asafswisa/leumi:latest'
        }
    }

    stage ("Login+push to ECR") {
        agent {label 'agent1'}
        steps{
            withENV (["AWS_ACCESS_KEY_ID=${env.AWS_ACCESS_KEY_ID}","AWS_SECRET_KEY=${env.AWS_SECRET_KEY}", "AWS
            DEFAULT_REGION=${env.AWS_DEFAULT_REGION}"])
            sh 'sudo docker login -u AWS -p $(aws ecr-public get-login-password --region us-east-1) public.ecr.aws/l6w1c8s9'
            sh 'docker build -t leumi .'
            sh 'docker tag leumi:latest public.ecr.aws/l6w1c8s9/leumi:latest'
            sh 'docker push public.ecr.aws/l6w1c8s9/leumi:latest'
        }
    }

    stage('deploy to EKS')
        agent(label 'agent2')







}