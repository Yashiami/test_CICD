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
				docker build -t nodemain:v1.0 .
				docker save -o nodemain.tar nodemain:v1.0
			}
		}
		stage("Deploy") {
			steps {
				docker load -i nodemain.tar
				docker run -d --expose 3000 -p 3000:3000 nodemain:v1.0
			}
		}
	}
}
	
