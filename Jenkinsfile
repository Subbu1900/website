pipeline{
    agent any
    //environment {
    //    DOCKERHUB_CREDENTIALS=credentials('36055715-431a-4dc3-81fe-c0df2f7f1b9e')
    //}
    environment {
registry = "ashdockash/upmi"
registryCredential = 'ashdockash'
dockerImage = ''
}
    
    stages{
        stage('Hello'){
        
            steps{
                echo 'Hello World'
            }
        }
        stage('git'){

            steps{

                git'https://github.com/Subbu1900/website.git'
            }
        }
        stage('docker') {

            steps {

                sh 'docker build /home/subrahmanyam/jenkins -t ashdockash/demo1'
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | sudo docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
                sh 'docker push ashdockash/demo1'

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
