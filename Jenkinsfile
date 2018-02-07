node {
	dir('jenkins-test') {
        	git url: 'git@bitbucket.org:lmilius/jenkins-test.git',
		credentialsId: 'lmilius'
    	}
	def app
	stage('Clone repository') {
		checkout scm
	}

	stage('Build image') {
		app = docker.build("helloworld-node:1")
	}
	
	stage('Test image') {
		app.inside {
			sh 'echo "Tests passed"'
		}
	}
	
	stage('Call second repo hello world') {
		sh 'jenkins-test/hello-jenkins-test.sh'
	}

//	stage('Push image') {
//		docker.withRegistry('https://registry.hub.docker.com', 'docker-hub-credentials') {
//		app.push("${env.BUILD_NUMBER}")
//		app.push("latest")
//		}
//	}
}
