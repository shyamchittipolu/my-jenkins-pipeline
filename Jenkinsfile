#!/usr/bin/env groovy
pipeline {
    agent any
    environment {
        AWS_ACCESS_KEY_ID = credentials('AWS_ACCESS_KEY_ID')
        AWS_SECRET_ACCESS_KEY = credentials('AWS_SECRET_ACCESS_KEY')
        AWS_DEFAULT_REGION = "eu-west-3"
    }
    stages {
        stage("Create an EKS Cluster") {
            steps {
                script {
                    sh 'mkdir -p EKSBuildPipeline3'
                    sh 'mkdir -p /var/lib/jenkins/workspace/EKSBuildPipeline3'

                    // Verify that the directory was created successfully
                    sh 'ls -ld /var/lib/jenkins/workspace/EKSBuildPipeline3'

                    // Copy files into the directory
                    sh 'cp -r EKSBuildPipeline EKSBuildPipeline1 EKSBuildPipeline2 EKSBuildPipeline3 EKSBuildPipeline@tmp Jenkinsfile backend.tf eks.tf kubernetes terraform terraform.tfvars terraform@tmp variables.tf vpc.tf /var/lib/jenkins/workspace/EKSBuildPipeline3/'

                // Run Terraform commands within the target directory
                    dir('/var/lib/jenkins/workspace/EKSBuildPipeline3') {
                            sh "terraform init"
                            sh "terraform apply -auto-approve"
                        }
                }
            }
        }
        stage("Deploy to EKS") {
            steps {
                script {
                    dir('kubernetes') {
                        sh "aws eks update-kubeconfig --name my-eks-cluster"
                        sh "kubectl apply -f nginx-deployment.yaml"
                        sh "kubectl apply -f nginx-service.yaml"
                    }
                }
            }
        }
    }
}
