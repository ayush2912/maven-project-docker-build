pipeline{
	agent any

	tools{
		maven 'LOCAL_MAVEN'
	}

	parameters{
		 string(name:'tomcatwebapp_port', defaultValue:'8181', description:'Tomcat WebApp Port')
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
					sh "docker rm -f \$(docker ps -aq -f name=tomcatwebapp)"
					echo 'Old Docker container Deleted successfully'

					echo 'Starting Docker Container'
					sh "docker run --name tomcatwebapp -d -p ${params.tomcatwebapp_port}:8080 tomcatwebapp:${env.BUILD_ID}"
					echo "Docker Container started successfully at port : ${params.tomcatwebapp_port}"
				}
				failure{
					echo 'Deployment Failed!'
				}
			}
		}
	}
}
