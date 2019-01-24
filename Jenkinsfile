pipeline{
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
					echo 'Application Docker image built Successfully!'
					echo 'Application Docker image built Successfully!'
					sh "sudo docker run -d -p 8181:8080 tomcatwebapp:${env.BUILD_ID}"
				}
				failure{
					echo 'Deployment Failed!'
				}
			}
		}
	}
}
