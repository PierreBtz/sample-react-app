pipeline {
    options {
        buildDiscarder(logRotator(artifactNumToKeepStr: '5', numToKeepStr: '10'))
    }
    agent {
        kubernetes {
            label 'sample-react-app'
            yamlFile 'build-pod.yaml'
        }
    }
    environment {
        // this is for create-react-app test 
        CI="true"
    }
    stages {
        stage('Prepare') {
            steps {
                container('npm') {
                    sh 'npm install'
                }
            }
        }
        stage('Tests') {
            steps {
                container('npm') {
                    sh 'npm run test'
                }
            }
        }
        stage('Build ') {
            // building the production artifacts, not publishing them in the demo
            when { anyOf { branch 'master'; branch 'develop' } }
            steps {
                container('npm') {
                    sh 'npm run build'
                }
            }
        }
    }
}