pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                checkout scm
                sh 'echo "Building.."'
                sh 'date > foo.txt'
                stash includes: '**/*.txt', name: 'app' 
            }
        }
        stage('Test') {
            steps {
                unstash 'app'
                sh 'echo "Testing.."'
                sh 'cat foo.txt'
            }
        }
        stage('Deploy') {
            when {
              expression {
                currentBuild.result == null || currentBuild.result == 'SUCCESS' 
              }
            }
            steps {
                sh 'echo make publish'
            }
        }
    }
}
