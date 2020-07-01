node{
   stage('SCM Checkout')
   {
     git 'https://github.com/vk879299/CICD-pipeline'
   }
   stage('Compile-Package')
   {
   //    Get maven home path here
       def mvnHome =  tool name: 'maven', type: 'maven'   
       sh "${mvnHome}/bin/mvn package"
   } 
   stage('SonarQube Analysis') {
        def mvnHome =  tool name: 'maven', type: 'maven'
        withSonarQubeEnv('sonar') { 
          sh "${mvnHome}/bin/mvn sonar:sonar"
        }
    
    }
   stage ('Build Docker Image') {
     sh 'docker build -t kavi31/my-app:1 .'
   }
   
   stage('Push Docker image'){
   withCredentials([string(credentialsId: ' ', variable: 'docker_password')]) {
   sh "docker login -u kavi31 -p ${docker_password}"
}
  
   sh 'docker push kavi31/my-app:1'
}
}
