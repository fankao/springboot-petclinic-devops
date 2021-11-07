pipeline{
	agent any
	environment {
		DOCKERHUB_CREDENTIALS=credentials('dockerhub')
	}

 	stages {
     stage('Build'){
		steps{
			sh './mvnw clean install'
		}   
    }
     stage('Test'){
		 steps{
			 sh './mvnw test'
		 }
    }
		stage('Build Docker image') {
			steps {
				sh 'docker build -t 02039921/spring-petclinic-devops:latest .'
			}
		}
		stage('Login') {
			
		}

		stage('Push image to DockerHub') {
			steps {
				sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
				sh 'docker push 02039921/spring-petclinic-devops:latest'
			}
		}
	}

	post {
		always {
			sh 'docker logout'
		}
	}

}
