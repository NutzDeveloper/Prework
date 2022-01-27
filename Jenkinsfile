pipeline {
    agent {
        docker { image 'python:alpine' }
	}		
    stages {
		stage ('Preperation') {
			steps {
				echo "Installing Dependencies"
				sh 'pip3 install pytest'			
				}
		}
		stage ('Test') {
			steps {
				echo "Running test"
				sh 'python3 -m pytest app.py'
				}
			}
		stage ('Kubernetes')
		{
			steps 
			{
				script 
				{
					kubernetesDeploy(configs: "test.yaml", kubeconfigId: "kubeconfig")
				}
			}
		}
	}
		
		post
		{
			always 
			{
				echo " ======================= PIPELINE FINISHED ======================="
			}
			
			failure 
			{
				echo " ======================= PIPELINE FAILED ======================="
			}
			
			success
			{
				echo " ======================= PIPELINE SUCCESSFUL ======================="
			}
		}


    }

