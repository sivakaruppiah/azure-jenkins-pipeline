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

    stage('Deploy') {
            steps {
                // login Azure
                  withCredentials([azureServicePrincipal('server-principal')]) {
                  sh 'az login --service-principal -u $AZURE_CLIENT_ID -p $AZURE_CLIENT_SECRET -t $AZURE_TENANT_ID'
                  }
               // get publish settings
            }
        }
    stage('TF Plan') {
      steps {
        container('terraform') {
          sh 'terraform init'
          sh 'terraform plan -out myplan'
        }
      }      
    }

    stage('Approval') {
      steps {
        script {
          def userInput = input(id: 'confirm', message: 'Apply Terraform?', parameters: [ [$class: 'BooleanParameterDefinition', defaultValue: false, description: 'Apply terraform', name: 'confirm'] ])
        }
      }
    }

    stage('TF Apply') {
      steps {
        container('terraform') {
          sh 'terraform apply -input=false myplan'
        }
      }
    }

  } 

}
