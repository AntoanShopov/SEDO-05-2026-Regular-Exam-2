pipeline {
    agent any

    triggers {
        pollSCM('* * * * *')
    }

    stages {
        stage('Restore dependencies') {
            when {
                branch 'main'
            }
            steps {
                script {
                    if (isUnix()) {
                        sh 'dotnet restore Homies.sln'
                    } else {
                        bat 'dotnet restore Homies.sln'
                    }
                }
            }
        }

        stage('Build application') {
            when {
                branch 'main'
            }
            steps {
                script {
                    if (isUnix()) {
                        sh 'dotnet build Homies.sln --configuration Release --no-restore'
                    } else {
                        bat 'dotnet build Homies.sln --configuration Release --no-restore'
                    }
                }
            }
        }

        stage('Run all tests') {
            when {
                branch 'main'
            }
            steps {
                script {
                    if (isUnix()) {
                        sh 'dotnet test Homies.sln --configuration Release --no-build'
                    } else {
                        bat 'dotnet test Homies.sln --configuration Release --no-build'
                    }
                }
            }
        }
    }
}
