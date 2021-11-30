#!groovy
pipeline {
    agent none

    stages {
        stage('Build') {
            agent {
                    docker {image 'node:17-bullseye'}
            }
            steps {
                dir('DotnetTemplate.Web') {
                    echo 'Building..'
                    sh 'node --version'
                    sh 'npm ci'
                    sh 'npm run build'
                    sh 'npm t'
                }
            }
        }
        stage('Test') {
            steps {
                echo 'Testing..'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
            }
        }
    }
}