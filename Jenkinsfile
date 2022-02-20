node {
	stage('Clone Repository') {
		checkout scm
	}    
    
	stage('Terraform Init') {
		sh 'terraform init'
	}
        
    stage('Terraform Plan') {
		withEnv(["AWS_SESSION_TOKEN=${aws_session_token}","AWS_ACCESS_KEY_ID=${aws_access_key_id}", "AWS_SECRET_ACCESS_KEY=${aws_secret_access_key}"]) {
			sh '''
        		terraform plan --out tfplan.binary
        		terraform show -json tfplan.binary | jq '.' > tfplan.json
			'''
		}
    }
        
    //stage('TF Plan Analysis') {
	//	sh 'checkov -f tfplan.json --bc-api-key ${bc-api-key} --output-bc-ids --repo-id ${repo-id}'
    //}
}
