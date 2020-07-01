node{
   stage('SCM Checkout'){
     git 'https://github.com/vk879299/CICD-pipeline'
   }
   stage('Compile-Package'){
   //    Get maven home path here
       def mvnHome =  tool name: 'M2_HOME', type: 'maven'   
       sh "${mvnHome}/bin/mvn package"
   } 
   
    stage('SonarQube Analysis') {
        def mvnHome =  tool name: 'M2_HOME', type: 'maven'
        withSonarQubeEnv('sonarrunner') { 
          sh "${mvnHome}/bin/mvn sonar:sonar"
        }
    }
    
    stage ('Build Docker Image') {
     sh 'docker build -t kaveri/my-app:1 .'
   }
   
   stage('Push Docker image'){
   withCredentials([string(credentialsId: 'docker_password', variable: 'docker_password')]) {
   sh "docker login -u kaveri -p ${docker_password}"
}
  
   sh 'docker push kaveri/my-app:1'
   
   
   
   }
   stage ('Deploy Pod to Kubernetees Cluster'){
          
    	 kubernetesDeploy(configs: 'deployment.yaml',kubeconfigId: 'kubernetesid')
               		
            		
   }
   stage ('Terraform Init') {
      print "Initialize Provider" 
      sh "terraform init"
    }


    stage ('Terraform Validate') {
      print "Validating  Files"
      sh "terraform validate"
    }
    
    stage ('Terraform Plan') {
             sh """
        set +x
        terraform plan  -out=s3b.tfplan
        """ 
                    }  
    

  
    stage ('Terraformm  Apply') {
      
        sh """
        set +x
        terraform apply s3b.tfplan
        """
       }  
    
   }


     
