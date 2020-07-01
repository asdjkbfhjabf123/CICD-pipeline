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
   
   stage('Sonarqube')
   {
    environment 
      {
        scannerHome = tool 'sonarrunner'
      }
    steps
      {
        withSonarQubeEnv('sonarqube') 
         {
            sh "${scannerHome}/bin/sonar-scanner"
         }
        timeout(time: 10, unit: 'MINUTES') 
         {
            waitForQualityGate abortPipeline: true
         }
     }
  }
}
