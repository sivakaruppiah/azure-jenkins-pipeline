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
    sh '''export ARM_CLIENT_ID="4e7c311e-0bad-4c62-a960-fae95d64609f"
          export ARM_CLIENT_SECRET="DLEs978XWH99CqQm~2ZuV~NlULKAbYG~Vq"
          export ARM_SUBSCRIPTION_ID="423777e6-d2d1-4457-be29-3d98b3cd537c"
          export ARM_TENANT_ID="17c6997b-f6d9-4a44-8ddd-800751c7ebdd"
          terraform init'''
    }


    stage('init') {
    sh '''export ARM_CLIENT_ID="4e7c311e-0bad-4c62-a960-fae95d64609f"
          export ARM_CLIENT_SECRET="DLEs978XWH99CqQm~2ZuV~NlULKAbYG~Vq"
          export ARM_SUBSCRIPTION_ID="423777e6-d2d1-4457-be29-3d98b3cd537c"
          export ARM_TENANT_ID="17c6997b-f6d9-4a44-8ddd-800751c7ebdd"
          terraform plan'''
    }


    stage('init') {
    sh '''export ARM_CLIENT_ID="4e7c311e-0bad-4c62-a960-fae95d64609f"
          export ARM_CLIENT_SECRET="DLEs978XWH99CqQm~2ZuV~NlULKAbYG~Vq"
          export ARM_SUBSCRIPTION_ID="423777e6-d2d1-4457-be29-3d98b3cd537c"
          export ARM_TENANT_ID="17c6997b-f6d9-4a44-8ddd-800751c7ebdd"
          terraform apply -auto-approve'''
    }


    

  } 

}
