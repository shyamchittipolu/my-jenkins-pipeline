t#!/usr/bin/env groovy
pipeline {
    agent any
    environment {
        AWS_ACCESS_KEY_ID = credentials('AWS_ACCESS_KEY_ID')
        AWS_SECRET_ACCESS_KEY = credentials('AWS_SECRET_ACCESS_KEY')
        AWS_DEFAULT_REGION = "eu-west-3"
    }
    stages {
        
                            sh "terraform init"
                            sh "terraform destroy -auto-approve"
                        }
                }
            }
        }
   
