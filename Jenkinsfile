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
    
    stages {
        stage('Clone Repository') {
            checkout scm
        }
        
        stage('Terraform Init') {
            script {
	              sh "terraform init"
            }
        }
        
        stage('Terraform Plan') {
            script {
                sh "terraform plan --out tfplan.binary"
                sh "terraform show -json tfplan.binary | jq '.' > tfplan.json"
            }
        }
        
        stage('TF Plan Analysis') {
            script {
                sh "checkov -f tfplan.json --bc-api-key ${bc-api-key} --output-bc-ids --repo-id ${repo-id}"
            }
        }
    }
}
