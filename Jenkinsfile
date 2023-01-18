pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
		withCredentials([usernamePassword(credentialsId: 'docker-hub', passwordVariable: 'password', usernameVariable: 'username')]) {
                sh "docker build -t rufatzakirov/sharks:v$BUILD_ID ."
		sh "docker push rufatzakirov/sharks:v$BUILD_ID"
		}
            }
        }
	stage('Deploy') {
            steps {
                sh "docker run -d --name sharks-$BUILD_ID -p 80$BUILD_ID:8080 rufatzakirov/sharks:v$BUILD_ID"
            }
    }
}
}
