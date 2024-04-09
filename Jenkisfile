pipeline {
    agent any
    tools {
        maven 'maven3.9'
        jdk 'java17'
    }
    stages {
        stage('git-code-download') {
            steps {
                echo "Downloading code from git"
                git branch: 'main', url: 'https://github.com/devopstechlab/jenkins2-maven.git'
            }
        } 
        stage('Build') {
            steps {
                echo "Going to start Java Project Build using maven"
                sh 'mvn clean package'
            }
        } 
        stage('Test-Case-Report') {
            steps {
                echo "Let's check trend analysis of junit report"
                junit stdioRetention: '', testResults: '**/target/surefire-reports/*.xml'
            }
        } 
        stage('Archive-Artifacts') {
            steps {
                echo "Archiving the artifacts"
                archiveArtifacts artifacts: '**/*.war', followSymlinks: false
            }
        } 
        stage('Deploy-to-Dev') {
            steps {
                build wait: false, job: 'deploy-dev-pipeline'
            }
        } 
    }
}
