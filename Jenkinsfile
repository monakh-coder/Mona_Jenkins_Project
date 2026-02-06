pipeline {
    agent any

    stages {

        stage('Mona-Verify Branch') {
            steps {
                echo "Current branch: ${env.GIT_BRANCH}"
            }
        }

        stage('Mona- Build Docker Image') {
            steps {
                dir("${env.WORKSPACE}/azure-vote") {
                    sh 'docker compose build'
                }
            }
        }

        stage('Mona- Login to Dockerhub') {
            steps {
                withCredentials([
                    usernamePassword(
                        credentialsId: 'dockerhub',
                        usernameVariable: 'DH_USER',
                        passwordVariable: 'DH_PASS'
                    )
                ]) {
                    sh '''
                        echo "$DH_PASS" | docker login -u "$DH_USER" --password-stdin
                    '''
                }
            }
        }

        stage('Mona- Push Image to Dockerhub') {
            steps {
                dir("${env.WORKSPACE}/azure-vote") {
                    sh 'docker compose push'
                }
            }
        }
    }
}
