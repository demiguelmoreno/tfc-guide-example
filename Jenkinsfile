node {
	environment {
	        AWS_ACCESS_KEY_ID = ${aws-access-key-id}
		AWS_SECRET_ACCESS_KEY = ${aws-secret-access-key}
		AWS_SESSION_TOKEN = ${aws-session-token}
	}
	
	stage('Clone Repository') {
		checkout scm
	}    
    
	stage('Terraform Init') {
		sh 'terraform init'
	}
        
    stage('Terraform Plan') {
	sh "export AWS_ACCESS_KEY_ID=${AWS_ACCESS_KEY_ID}"
	echo "${AWS_ACCESS_KEY_ID}"
	sh 'printenv'
        //sh 'terraform plan --out tfplan.binary'
        //sh "terraform show -json tfplan.binary | jq '.' > tfplan.json"
    }
        
    //stage('TF Plan Analysis') {
	//	sh 'checkov -f tfplan.json --bc-api-key ${bc-api-key} --output-bc-ids --repo-id ${repo-id}'
    //}
}
