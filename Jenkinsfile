pipeline{
   //agent any
   agent {label 'worker'}
   options{
    buildDiscarder(logRotator(numToKeepStr: '15'))
    disableConcurrentBuilds()
    retry(2)
    timeout(time: 1, unit: 'MINUTES')
   }
   parameters{
    string(name: 'BRANCH', defaultValue: 'master')
   }
   stages{
    stage('Build and Push'){
        steps{
            sh '''
            aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin 732275424814.dkr.ecr.us-east-1.amazonaws.com
            cd app
            docker build -t ameya -f Dockerfile.txt .
			docker tag ameya:latest 732275424814.dkr.ecr.us-east-1.amazonaws.com/ameya:latest
            docker push 732275424814.dkr.ecr.us-east-1.amazonaws.com/ameya:latest
			docker run -itd -p 8081:8081 732275424814.dkr.ecr.us-east-1.amazonaws.com/ameya:latest
            '''
        }
    }
    stage('Deploy Stage'){
        steps{
            sh "sleep 5"
        }
    }
   }
   }
