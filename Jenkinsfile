
pipeline {

  agent {
    node {
        label 'k8-worker-02'
        
    }
}

  stages {

    stage('Checkout Source') {
      steps {
        git url:'https://github.com/sivakaruppiah/azure-jenkins-pipeline.git', branch:'master'
      }
    }

    stage('init') {
      steps { 
            // login Azure
                  withCredentials([azureServicePrincipal('server-principal')]) {
                  sh '''export ARM_CLIENT_ID=$AZURE_CLIENT_ID
                        export ARM_CLIENT_SECRET=$AZURE_CLIENT_SECRET
                        export ARM_SUBSCRIPTION_ID=$ARM_SUBSCRIPTION_ID
                        export ARM_TENANT_ID=$AZURE_TENANT_ID
                        terraform init'''
                  }
               // get publish settings 
        
       }   
    }

    

    stage('plan') {
      steps {  
            // login Azure
                  withCredentials([azureServicePrincipal('server-principal')]) {
                  sh '''export ARM_CLIENT_ID=$AZURE_CLIENT_ID
                        export ARM_CLIENT_SECRET=$AZURE_CLIENT_SECRET
                        export ARM_SUBSCRIPTION_ID=$ARM_SUBSCRIPTION_ID
                        export ARM_TENANT_ID=$AZURE_TENANT_ID
                        terraform plan'''
                  }
               // get publish settings 
       }   
    }


    stage('apply') {
      steps {  
            // login Azure
                  withCredentials([azureServicePrincipal('server-principal')]) {
                  sh '''export ARM_CLIENT_ID=$AZURE_CLIENT_ID
                        export ARM_CLIENT_SECRET=$AZURE_CLIENT_SECRET
                        export ARM_SUBSCRIPTION_ID=$ARM_SUBSCRIPTION_ID
                        export ARM_TENANT_ID=$AZURE_TENANT_ID
                        terraform apply -auto-approve'''
                  }
               // get publish settings 
       }   
    }


    

  } 

}
