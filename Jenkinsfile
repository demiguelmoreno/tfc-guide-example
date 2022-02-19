node {
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
    stage('Clone Repository') {
		checkout scm
	}    
    
	stage('Terraform Init') {
		sh "terraform init"
	}
        
    stage('Terraform Plan') {
		sh "export AWS_ACCESS_KEY_ID=${aws-access-key-id}"
		sh "export AWS_SECRET_ACCESS_KEY=${aws-secret-access-key}"
		sh "export AWS_SESSION_TOKEN=${aws-session-token}"
		echo "DATA1: ${aws-access-key-id}"
		echo "DATA2: ${aws-secret-access-key}"
		echo "DATA3: ${aws-session-token}"
		echo "---------------------------------------"
		sh 'printenv'
		echo "---------------------------------------"
        sh "terraform plan --out tfplan.binary"
        sh "terraform show -json tfplan.binary | jq '.' > tfplan.json"
    }
        
    stage('TF Plan Analysis') {
		sh "checkov -f tfplan.json --bc-api-key ${bc-api-key} --output-bc-ids --repo-id ${repo-id}"
    }
    }
}
