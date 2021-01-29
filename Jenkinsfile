pipeline{
    agent any 
    tools {
        "org.jenkinsci.plugins.terraform.TerraformInstallation" "terraform"
    }
    environment {
        TF_HOME = tool('terraform')
        TF_IN_AUTOMATION = "true"
        PATH = "$TF_HOME:$PATH"
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
                  sh '''

                        echo "Initialising Terraform"
                        terraform init 
                        '''
                  }
               // get publish settings 
        
       }   
    }

    stage('Terraform Validate'){
      steps { 
            // login Azure
                  withCredentials([azureServicePrincipal('server-principal'), string(credentialsId: 'access_key', variable: 'AZURE_ACCESS_KEY')]) {
                         sh '''
                                
                        terraform validate
                        '''                 }
               // get publish settings 
        
       }   
    }
    
        
    stage('Terraform Plan'){
      steps { 
            // login Azure
                  withCredentials([azureServicePrincipal('server-principal'), string(credentialsId: 'access_key', variable: 'AZURE_ACCESS_KEY')]) {
                        sh '''
                        export ARM_CLIENT_ID=$AZURE_CLIENT_ID
                        export ARM_CLIENT_SECRET=$AZURE_CLIENT_SECRET
                        export ARM_SUBSCRIPTION_ID=$AZURE_SUBSCRIPTION_ID
                        export ARM_TENANT_ID=$AZURE_TENANT_ID
                        echo "Creating Terraform Plan"
                        terraform plan 
                        '''
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
                        sh '''
                        export ARM_CLIENT_ID=$AZURE_CLIENT_ID
                        export ARM_CLIENT_SECRET=$AZURE_CLIENT_SECRET
                        export ARM_SUBSCRIPTION_ID=$AZURE_SUBSCRIPTION_ID
                        export ARM_TENANT_ID=$AZURE_TENANT_ID
                        echo "Applying the plan"
                        terraform apply -auto-approve 
                        '''
                  }
               // get publish settings 
       }   
    }


    

  } 

}
