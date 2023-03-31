pipeline{

	environment {
		DOCKERHUB_CREDENTIALS=credentials('jenkins-dockerhub')
	}

	agent any

	stages {
		stage('gitclone') {

			steps {
				git branch: 'main', url: 'https://github.com/jose-10000/app-grupo3.git'
			}
		}

		stage('Build') {

			steps {
				echo 'Building..'
				sh 'docker build -t jose10000/grupo3-app:v1.$BUILD_NUMBER .'
			}
		}

		stage('Login') {

			steps {
				sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
			}
		}

		stage('Push') {

			steps {
				sh 'docker push jose10000/grupo3-app:v1.$BUILD_NUMBER'
			}
		}
	}

	post {
		always {
			sh 'docker rmi $(docker images -a -q)'
			sh 'docker logout'

		}
	}

}

