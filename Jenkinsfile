pipline {
    agent none

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
            sh 'docker build -t leumi1 .'
            sh 'docker tag lemi1:latest 349384651398.dkr.ecr.eu-central-1.amazonaws.com/lemi1:latest'
            sh 'docker push 349384651398.dkr.ecr.eu-central-1.amazonaws.com/lemi1:latest'
        }
    }

    stage('deploy to EKS')
        agent(label 'agent2')
        steps {
            sh 'kubectl apply -y /home/ubuntu/jenkins/deployment.yaml'
        }







}