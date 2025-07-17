pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // Pull the latest code from GitHub
                git 'https://github.com/farhanaleey/flask-app.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                // Build Docker image and tag it
                script {
                    dockerImage = docker.build("your-dockerhub-username/flask-app:latest")
                }
            }
        }

        stage('Run Tests') {
            steps {
                // Run any tests here, for now just echo
                sh 'echo Running tests...'
            }
        }

        stage('Push Image') {
            steps {
                // Log in to DockerHub and push image
                withCredentials([usernamePassword(credentialsId: 'dockerhub-creds', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                    sh 'docker login -u $DOCKER_USER -p $DOCKER_PASS'
                    sh 'docker push khan/flask-app:latest'
                }
            }
        }

        stage('Deploy') {
            steps {
                // For demo: just echo deploy step
                sh 'echo Deploying application...'
                // Here you can add kubectl commands to deploy to Kubernetes
            }
        }
    }
}
