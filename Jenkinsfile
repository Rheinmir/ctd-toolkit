pipeline {
    agent { label 'dockerlinux' }

    triggers {
        githubPush()
    }

    stages {
        stage('Pull Source') {
            steps {
                sh 'git status'
            }
        }
        stage('Build & Deploy') {
            steps {
                sh """
                docker stop ctd-toolkit-prd || true
                docker rm ctd-toolkit-prd || true
                docker rmi ctd-toolkit-img || true
                docker build -t ctd-toolkit-img .
                docker run -d --name ctd-toolkit-prd -p 8180:80 ctd-toolkit-img
                """
            }
        }
    }
}
