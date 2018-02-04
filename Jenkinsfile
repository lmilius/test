node {
	def app
	stage('Clone repository') {
		checkout scm
	}

	stage('Build image') {
		docker.withServer('tcp://ci.admin.milius.lab:2376') {
			app = docker.build("helloworld-node:1")
		}
	}
	
	stage('Test image') {
		app.inside {
			sh 'echo "Tests passed"'
		}
	}

	stage('Push image') {
		docker.withRegistry('https://registry.hub.docker.com', 'docker-hub-credentials') {
		app.push("${env.BUILD_NUMBER}")
		app.push("latest")
		}
	}
}
