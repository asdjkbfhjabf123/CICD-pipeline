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
   
}
