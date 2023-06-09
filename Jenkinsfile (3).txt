pipeline {
    agent any
    environment {
      MY_CRED = credentials('c1de710d-a52b-4c8c-9196-0f24a0dd5194')
    }
  
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', credentialsId: '10fedfbb-8a4e-4700-b3cd-3ad56c87c166', url: 'https://github.com/obabaldbiyat/Prod_Custom-Nginx-server-Terraform_Azure_GitSourc'
            }
        }
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', credentialsId: '10fedfbb-8a4e-4700-b3cd-3ad56c87c166', url: 'https://github.com/obabaldbiyat/Staging_Custom-Nginx-server-Terraform_Azure_GitSourc'
            }
        }
        stage('conection') {
            steps {
               sh 'az login --service-principal -u $MY_CRED_CLIENT_ID -p $MY_CRED_CLIENT_SECRET -t $MY_CRED_TENANT_ID'
      }
    }
        stage('Terraform init') {
            steps {
                sh 'terraform init'
            }
        }
        stage('Terraform apply') {
            steps {
                sh 'terraform apply --auto-approve'
            }
        }
        
    }
}
