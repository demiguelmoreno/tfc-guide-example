node {
	stage('Clone Repository') {
		checkout scm
	}    
    
	stage('Terraform Init') {
		sh 'terraform init'
	}
        
	stage('Test AWS Credentials') {
	    sh '''
	        echo '[330803171396_AWSAdministratorAccess]' > .aws/credentials
	        echo "aws_access_key_id=${AWS_ACCESS_KEY_ID}" >> .aws/credentials
	        echo "aws_secret_access_key=${AWS_SECRET_ACCESS_KEY}" >> .aws/credentials
	        echo "aws_session_token=${AWS_SESSION_TOKEN}" >> .aws/credentials
	    '''
	}
	
	stage('AWS Configure') {
		sh 'aws configure'
	}
	
    stage('Terraform Plan') {
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
