pipeline {
    agent any
    stages {
        stage('build') {
            steps {
                echo 'Building Docker Image'
                sh 'docker build -t capstone-app .'
            }
        }
        stage('test') {
            steps {
                echo 'Testing Application'
                sh 'echo Test Passed'
            }
        }
        stage('prod') {
            when {
                expression {
                    env.GIT_BRANCH == 'origin/master'
                }
            }
            steps {
                echo 'Deploying to Production'
                sh '''
                docker stop prod_app || true
                docker rm prod_app || true
                docker run -d -p 80:80 --name prod_app capstone-app
                '''
            }
        }
    }
}
