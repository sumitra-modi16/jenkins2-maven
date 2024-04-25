pipeline {
    agent any
    stages {
        stage('git-code-download') {
            steps {
                echo "Downloading code from git"
                git branch: 'main', url: 'https://github.com/sumitra-modi16/jenkins2-maven.git'
            }
        } 
        stage('Build') {
            steps {
            	sh '''
		docker build -t skmodi123/myweb:${BUILD_NUMBER} .
		docker tag skmodi123/myweb:${BUILD_NUMBER} skmodi123/myweb:latest
		docker push skmodi123/myweb:${BUILD_NUMBER}
		docker push skmodi123/myweb:latest
		'''
            }
        } 
    }
}
