pipeline {
    agent any

    stages {

        stage("clone") {
            steps {
                git credentialsId: "github-token-creds", url: "https://github.com/Baisalov24/testapp.git", branch: 'main'
            }

        }
        stage ("Build image") {
            steps {
                sh 'docker build -t headphone-app:latest .'
            }
        }
        stage ("Deploy") {
            steps {
                sh '''
                docker stop headphone-app || true
                docker rm headphone-app || true

                docker run -d \\
                  --name headphone-app \\
                  -p 8081:80 \\
                  headphone-app:latest
                '''
            }
        }
    }
}