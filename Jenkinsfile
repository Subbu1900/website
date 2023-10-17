pipeline{
    agent any
    //environment {
    //    DOCKERHUB_CREDENTIALS=credentials('36055715-431a-4dc3-81fe-c0df2f7f1b9e')
    //}
    environment {
registry = "ashdockash/vs1"
registryCredential = 'docker_id'
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
        stage('Package'){
            steps{
                sh 'tar -czf myproj.tar.gz index.html images/'
                archiveArtifacts artifacts: 'myproj.tar.gz',allowEmptyArchive:false
            }
        }
        stage('Building image') {
steps{
    sh 'docker build -t pro1:latest -f /home/subrahmanyam/Gitproject/website .'
script {
dockerImage = docker.build registry + ":$BUILD_NUMBER"
}
}
}
stage('Deploy image') {
steps{
   // sshagent(['gitkey1']){
     //   sh 'docker save myapp:latest "docker load"'}
script {
docker.withRegistry( '', registryCredential ) {
dockerImage.push()
}
}
}
}
stage('Cleaning up') {
steps{
sh "docker rmi $registry:$BUILD_NUMBER"
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
