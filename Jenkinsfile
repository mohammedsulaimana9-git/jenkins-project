pipeline{
    agent any
    environment {
        IMAGE_NAME = "react-app"
        CONT_NAME = "react-app-cont"
    }
    stages{
        stage("Install"){
            steps{
                sh 'npm install'
            }
            }
    
     stage("Build"){
            steps{
                sh 'npm run build'
            }
     }
      stage("Docker login"){
            steps{
                 withDockerRegistry(credentialsId: 'Docker-Cred', url: 'https://index.docker.io/v1/
') {
          }
         }
            }
       stage("Build And push Image"){
            steps{
                sh '''
                docker build -t sulaiman/$IMAGE_NAME:latest -f Dockerfile1 .
                
                '''
            }
     }
     stage("Run Container"){
            steps{
                sh ''' 
                docker stop $CONT_NAME
                docker rm $CONT_NAME
                docker run -d -p 3000:80 --name $CONT_NAME sulaiman/$IMAGE_NAME:latest'''
            }
     }
}
    post{
        always{
            echo "========always========"
        }
        success{
            echo "========pipeline executed successfully ========"
        }
        failure{
            echo "========pipeline execution failed========"
        }
    }
 }
