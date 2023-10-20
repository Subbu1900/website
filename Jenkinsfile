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
    
        stage('git'){

            steps{

                git'https://github.com/Subbu1900/website.git'
            }
        }
        stage('SonarQube Analysis'){
            steps{
             withSonarQubeEnv('SonarQubeServer') { 
                    script {
                        def scannerHome = tool 'sonar';
                        withEnv(["PATH+SONAR=${scannerHome}/bin"]) {
                            sh 'sonar-scanner -Dsonar.projectKey=demoproj -Dsonar.sources=. -Dsonar.host.url=http://localhost:9000 -Dsonar.login=sqp_d239d86d91e3d3548e348bb174cddf84caef8bed'
                        }
                    }
                }
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
   // sh 'docker build -t pro1:latest -f /home/subrahmanyam/Gitproject/website .'
    sh 'docker build -t pro1:latest -f $WORKSPACE/Dockerfile $WORKSPACE/'
script {
dockerImage = docker.build registry + ":$BUILD_NUMBER"
}
}
}
stage('Deploy image') {
steps{
sh 'docker save -o latimg.tar pro1:latest;docker load -i latimg.tar'    
    // sshagent(['gitkey1']){
     //   sh 'docker save myapp:latest "docker load"'}
//script {
//docker.withRegistry( '', registryCredential ) {
//dockerImage.push()
//}
//}
}
}
        stage('Run Docker container'){
            steps{
         sh '''
                    container_ids=$(docker ps -a | grep 82 | awk \'{print $1}\')
                    if [ -n "$container_ids" ]; then
                        for container_id in $container_ids; do
                            docker stop "$container_id"
                            docker rm "$container_id"
                        done
                    else
                        echo "No containers found running on port 82."
                    fi
                    '''

            sh 'docker run -d -p 82:80 pro1:latest'}
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
