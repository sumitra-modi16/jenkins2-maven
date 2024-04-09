pipeline {
    agent any
    tools{
        maven 'maven3.9'
        jdk 'java17'
    }
    stages {
        stage('git-code-download') {
            steps {
                echo "downloading code from git"
                git branch: 'main', url: 'https://github.com/sumitra-modi16/jenkins2-maven.git'
            }
        }
        stage('build') {
            steps {
                echo "going to start java project build using maven"
                sh 'mvn clean package'
            }
        }
        stage('test-case-report') {
            steps {
                echo "let's check trent analysis"
                junit stdioRetention: '', testResults: '**/target/surefire-reports/*.xml'
            }
        }
        stage('archive-artifacts') {
            steps {
                echo "archiving the artifacts"
                archiveArtifacts artifacts: '**/*.war', followSymlinks: false
            }
        }
        stage('deploy-dev-auto-build') {
            steps {
                echo "deploy-dev-auto-build"
                build wait: false, job: 'deply-dev-pipeline'
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
