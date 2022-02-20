node {
	stage('Clone Repository') {
		checkout scm
	}    
    
	stage('Terraform Init') {
		sh 'terraform init'
	}
        
    stage('Terraform Plan') {
		withCredentials([[$class: 'AmazonWebServicesCredentialsBinding',
    		credentialsId: "aws-credentials",
    		accessKeyVariable: 'AWS_ACCESS_KEY_ID',
    		secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']]) {
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
