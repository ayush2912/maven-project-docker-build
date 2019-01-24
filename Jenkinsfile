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

					echo 'Deleting Old Docker container...'
					sudo docker rm -f $(sudo docker ps -aq -f name=tomcatwebapp)
					echo 'Old Docker container Deleted successfully'

					echo 'Starting Docker Container'
					sh "docker run --name tomcatwebapp -d -p 8181:8080 tomcatwebapp:${env.BUILD_ID}"
					echo "Docker Container started successfully at port : 8${env.BUILD_ID}8${env.BUILD_ID}"
				}
				failure{
					echo 'Deployment Failed!'
				}
			}
		}
	}
}
