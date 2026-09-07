pipeline {
    agent any
	stages {
		stage("Build") {
			steps {
				npm install
			}
		}
		stage("Test") {
			steps {
				npm test
			}
		}
		stage("Docker build") {
			steps {
				docker build -t nodedev:v1.0 .
				docker save -o nodedev.tar nodedev:v1.0
			}
		}
		stage("Deploy") {
			steps {
				docker load -i nodedev.tar
				docker ps -q | xargs -r docker rm -f
				docker run -d --expose 3001 -p 3001:3000 nodedev:v1.0.
			}
		}
	}
}
	
