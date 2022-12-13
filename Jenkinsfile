pipeline {
    agent any
          tools
    {
       maven "Maven 3.6.3"
    }
   
 stages {
      stage('checkout') {
           steps {
             
                git branch: 'master', url: 'https://github.com/YASHODA-MUNNANGI/JavaProject.git/'
             
          }
        }
  stage('Execute Maven') {
           steps {
             
                sh 'mvn package'             
          }
        }
stage('Docker Build and Tag') {
           steps {
              
                sh 'docker build -t samplewebapp:latest .' 
                sh 'docker tag samplewebapp Yashoda/samplewebapp:latest'
                
          }
        }
     
  stage('Publish image to Docker Hub') {
          
            steps {
        withDockerRegistry([ credentialsId: "dockerHub", url: "https://hub.docker.com/" ]) {
          sh  'docker push Yashoda/samplewebapp:latest'
         
        }
                  
          }
        }
     
      
 stage('Run Docker container on remote hosts') {
             
            steps {
                sh "docker -H ssh://jenkins@3.112.216.73 run -d -p 8003:8080 Yashoda/samplewebapp"
 
            }
        }
    }
 }
