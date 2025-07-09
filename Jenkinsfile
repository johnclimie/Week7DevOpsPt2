pipeline{
  agent any
  stages{
    stage('checkout'){
      steps{
        git branch: 'main', url: 'https://github.com/johnclimie/Week7DevOpsPt2'
      }
    }
    stage('Login to ECR'){
      steps{
        withAWS(region: 'us-east-2', credentials: 'aws-creds'){
          powershell '''
            $password = aws ecr get-login-password --region us-east-2
            docker login --username AWS --password $password 451947743265.dkr.ecr.us-east-2.amazonaws.com
          '''
        }
      }
    }
    stage('Build docker image'){
      steps{
        powershell '''
        docker build -t test:django
        docker tag test:django 451947743265.dkr.ecr.us-east-2.amazonaws.com/test:django
        '''
      }
    }
    stage('Pushing image to ECR'){
      steps{
        powershell '''
        docker push 451947743265.dkr.ecr.us-east-2.amazonaws.com/test:django
        '''
      }
    }
  }
}
