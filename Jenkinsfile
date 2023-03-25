pipeline{

	environment {
		DOCKERHUB_CREDENTIALS=credentials('jenkins-dockerhub')
	}

	agent any
	stages {
		stage('gitclone') {

			steps {
				git 'https://github.com/jose-10000/app-grupo3.git'
			}
		}

		stage('Build') {

			steps {
				sh 'docker build -t Yeivt/grupo3-app:v1.0 .'
			}
		}

		stage('Login') {

			steps {
				sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
			}
		}

		stage('Push') {

			steps {
				sh 'docker push Yeivt/grupo3-app:v1.0'
			}
		}
	}

	post {
		always {
			sh 'docker logout'
		}
	}

}

