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

    stage('Terraform Init'){
      steps { 
            // login Azure
                  withCredentials([azureServicePrincipal('server-principal'), string(credentialsId: 'access_key', variable: 'AZURE_ACCESS_KEY')]) {
                  sh """

                        echo "Initialising Terraform"
                        terraform init -backend-config="access_key=$AZURE_ACCESS_KEY"
                        """
                  }
               // get publish settings 
        
       }   
    }

    stage('Terraform Validate'){
      steps { 
            // login Azure
                  withCredentials([azureServicePrincipal('server-principal'), string(credentialsId: 'access_key', variable: 'AZURE_ACCESS_KEY')]) {
                         sh """
                                
                        terraform validate
                        """                  }
               // get publish settings 
        
       }   
    }
    
        
    stage('Terraform Plan'){
      steps { 
            // login Azure
                  withCredentials([azureServicePrincipal('server-principal'), string(credentialsId: 'access_key', variable: 'AZURE_ACCESS_KEY')]) {
                        sh """
                        
                        echo "Creating Terraform Plan"
                        terraform plan -var "ARM_CLIENT_ID=$AZURE_CLIENT_ID" -var "ARM_CLIENT_SECRET=$AZURE_CLIENT_SECRET" -var "ARM_SUBSCRIPTION_ID=$AZURE_SUBSCRIPTION_ID" -var "ARM_TENANT_ID=$AZURE_TENANT_ID"
                        """
                  }
               // get publish settings 
        
       }   
    }


    

    stage('Waiting for Approval'){
       steps {
                timeout(time: 10, unit: 'MINUTES') {
                    input (message: "Deploy the infrastructure?")
                }
        }
        
    }

    stage('Terraform Apply'){
      steps {  
            // login Azure
                  withCredentials([azureServicePrincipal('server-principal'), string(credentialsId: 'access_key', variable: 'AZURE_ACCESS_KEY')]) {
                        sh """
                        echo "Applying the plan"
                        terraform apply -auto-approve -var "ARM_CLIENT_ID=$AZURE_CLIENT_ID" -var "ARM_CLIENT_SECRET=$AZURE_CLIENT_SECRET" -var "ARM_SUBSCRIPTION_ID=$AZURE_SUBSCRIPTION_ID" -var "ARM_TENANT_ID=$AZURE_TENANT_ID"
                        """
                  }
               // get publish settings 
       }   
    }


    

  } 

}
