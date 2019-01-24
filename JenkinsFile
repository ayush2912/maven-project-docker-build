peline{
	agent any

	tools{
		maven 'LOCAL_MAVEN'
	}

	stages{

		stage('Build'){
			steps{
				sh 'mvn clean package'
				sh "docker build . -t tomcatwebapp:${env.BUILD_ID}"
			}
			post{
				success{
					echo 'Code Deployed Successfully!'
				}
				failure{
					echo 'Deployment Failed!'
				}
			}
		}
	}
}
