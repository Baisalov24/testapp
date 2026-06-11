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
                sh 'docker build -t timabai/headphone-app:latest .'
            }
        }
        stage ("Push") {
            steps {
                sh 'docker push timabai/headphone-app:latest'
            }
        }
        stage('Deploy') {
            steps {
                sh '''
                ssh -o StrictHostKeyChecking=no ubuntu@13.221.61.224 "
                docker pull timabai/headphone-app:latest &&
                docker stop website || true &&
                docker rm website || true &&
                docker run -d \
                --name website \
                -p 80:80 \
                timabai/headphone-app:latest
                "
                '''
            }
        }
         
    }
}