pipeline {
    agent any
   stages {
        stage('Verify Branch') { 
            steps {
                echo "$GIT_BRANCH"
                // Verify the branches and echo the current branch
            }
        }
         
        stage('Mona- Build Docker Image') {
            steps {
                sh 'docker compose build'
                // we have docker compose yaml so just need docker commose build to build the image
            }
        }
        stage("Mona- Login to Dockerhub") {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub', usernameVariable: 'DH_USER', passwordVariable: 'DH_PASS')]) {
                    sh """
                        echo "$DH_PASS" | docker login -u "$DH_USER" --password-stdin
                """
        }
      }
    }
   }
}
