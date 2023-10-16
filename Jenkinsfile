pipeline{
    agent any
    environment {
        DOCKERHUB_CREDENTIALS=credentials('36055715-431a-4dc3-81fe-c0df2f7f1b9e')
    }
    
    stages{
        stage('Hello'){
        
            steps{
                echo 'Hello World'
            }
        }
        stage('git'){

            steps{

                git'https://github.com/intellipaat2/website.git'
            }
        }
        stage('docker') {

            steps {

                sh 'sudo docker build /home/subrahmanyam/jenkins/workspace/pipeline -t ashdockash/demo1'
                sh 'sudo echo $DOCKERHUB_CREDENTIALS_PSW | sudo docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
                sh 'sudo docker push ashdockash/demo1'

            }
        }
        //stage('Kuberneets') {
          
         //   steps {

         //       sh 'sudo kubectl create -f deploy.yml'
         //       sh 'sudo kubectl create -f svc.yml'
         //   }
       // }        
        
    }
}
