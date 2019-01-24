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
					echo 'Starting Docker Container'
					sh "docker run -d -p 8${env.BUILD_ID}8${env.BUILD_ID}:8080 tomcatwebapp:${env.BUILD_ID}"
				}
				failure{
					echo 'Deployment Failed!'
				}
			}
		}
	}
}
