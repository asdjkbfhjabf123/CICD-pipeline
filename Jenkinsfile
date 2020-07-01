node{
   stage('SCM Checkout')
   {
     git 'https://github.com/vk879299/CICD-pipeline'
   }
   stage('Compile-Package')
   {
   //    Get maven home path here
       def mvnHome =  tool name: 'M2_HOME', type: 'maven'   
       sh "${mvnHome}/bin/mvn package"
   } 
   stage('SonarQube Analysis') {
        def mvnHome =  tool name: 'sonarscanner', type: 'sonar'
        withSonarQubeEnv('sonar') { 
          sh "/opt/sonarscanner sonarqube:sonarqube"
        }
    }
   
}
