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
    stages {
        stage('Prepare') {
            steps {
                container('npm') {
                    sh 'npm install'
                }
            }
        }
        stage('Build') {
            steps {
                container('npm') {
                    sh 'npm run build'
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
    }
}