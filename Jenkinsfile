pipeline {
    //agent {
    //    docker {
    //        image 'bridgecrew/jenkins_bridgecrew_runner:latest'
    //    }
    //}
    //stages {
    //    stage('test') {
    //        steps {
    //            script {
    //                sh "/run.sh ${token} ${Repo}"

    //            }
    //        }
    //    }
    //}
    //options {
    //    preserveStashes()
    //    timestamps()
    //    ansiColor('xterm')
    //}
    agent any
    stages {
        stage('Clone Repository') {
			steps {
				checkout scm
			}
        }
        
        stage('Terraform Init') {
			steps {
            	script {
	              sh "terraform init"
				}
            }
        }
        
        stage('Terraform Plan') {
			steps {
            	script {
                	sh "terraform plan --out tfplan.binary"
                	sh "terraform show -json tfplan.binary | jq '.' > tfplan.json"
            	}
			}
        }
        
        stage('TF Plan Analysis') {
			steps {
            	script {
                	sh "checkov -f tfplan.json --bc-api-key ${bc-api-key} --output-bc-ids --repo-id ${repo-id}"
            	}
			}
        }
    }
}
