pipeline {
    agent any
	tools {
		nodejs "node-7.8"
		dockerTool "docker-latest"
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
				sh '''docker build -t nodemain:v1.0 .
				docker save -o nodemain.tar nodemain:v1.0'''
			}
		}
		stage("Deploy") {
			steps {
				sh '''docker load -i nodemain.tar
				docker ps -q | xargs -r docker rm -f
				docker run -d --expose 3000 -p 3000:3000 nodemain:v1.0'''
			}
		}
	}
}
	
