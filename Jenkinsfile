#!groovy
pipeline {
    agent none

    environment {
        HOME = "/tmp" 
        DOTNET_CLI_HOME = "/tmp/DOTNET_CLI_HOME"
    }

    stages {
        stage('Do all builds') {
            parallel {
                stage('Build and Test NPM') {
                    agent {
                            docker { image 'node:17-bullseye' }
                    }
                    steps {
                        dir('DotnetTemplate.Web') {
                            echo 'Building..'
                            sh 'npm ci'
                            sh 'npm run build'
                            sh 'npm t'
                        }
                    }
                }
                stage('Build and Test Dotnet') {
                    agent {
                            docker { image 'mcr.microsoft.com/dotnet/sdk:latest' }
                    }
                    steps {
                        echo 'Building..'
                        sh 'dotnet build'
                        sh 'dotnet test'
                    }
                }
            }
        }
    }
}