pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Restore') {
            steps {
                sh 'dotnet restore Episememe-Test/Episememe-Test.sln'
            }
        }
        stage('Clean') {
            steps {
                sh 'dotnet clean Episememe-Test/Episememe-Test.sln'
            }
        }
        stage('Build') {
            steps {
                sh 'dotnet build Episememe-Test/Episememe-Test.sln -c release'
            }
        }
        stage('Test') {
            steps {
                echo 'Testing...'
            }
        }
        stage('Deploy') {
            when {
                expression {
                    currentBuild.result == null || currentBuild.result == 'SUCCESS' 
                }
            }
            steps {
                sh 'dotnet publish Episememe-Test/Episememe-Test.sln'
            }
        }
    }
}