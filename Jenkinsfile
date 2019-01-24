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
					echo "8`expr ${env.BUILD_ID} - 1`8`expr ${env.BUILD_ID} - 1`"
					sh "docker run -d -p ${env.BUILD_ID}${env.BUILD_ID}:8080 tomcatwebapp:${env.BUILD_ID}"
					echo "Docker Container started successfully at port : 8${env.BUILD_ID}8${env.BUILD_ID}"
				}
				failure{
					echo 'Deployment Failed!'
				}
			}
		}
	}
}
