pipeline {
    agent any
	tools {
		nodejs "node-7.8"
		docker "docker-latest"
	}
	stages {
		stage("Build") {
			steps {
				sh 'npm install --save-dev react-scripts@1.1.5'
			}
		}
		stage("Test") {
			steps {
				sh 'npm test'
			}
		}
		stage("Docker build") {
			steps {
				sh '''docker build -t nodedev:v1.0 .
				docker save -o nodedev.tar nodedev:v1.0'''
			}
		}
		stage("Deploy") {
			steps {
				sh '''docker load -i nodedev.tar
				docker ps -q | xargs -r docker rm -f
				docker run -d --expose 3001 -p 3001:3000 nodedev:v1.0.'''
			}
		}
	}
}
	
