pipeline {
    agent { label "test1" }
    stages {
        stage('Clone Code') {
            steps {
                echo 'Cloning the code from the repository...'
                git url: "https://github.com/rahultanwar8814/django-notes-app.git", branch: "master"
            }
        }
        
        stage('Build') {
            steps {
                echo 'Building the Docker image...'
                sh 'docker build -t notes-app:latest .'
            }
        }
        
        stage('Push to DockerHub') {
            steps {
                echo 'Pushing the image to DockerHub...'
                withCredentials([usernamePassword(credentialsId: "dockerHubCred", usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
                    sh 'docker login -u ${USERNAME} -p ${PASSWORD}'
                    sh 'docker tag notes-app ${USERNAME}/notes-app:latest'
                    sh 'docker push ${USERNAME}/notes-app:latest'
                }
            }
        }
        
        stage('Test') {
            steps {
                echo 'Running tests on the code...'
            }
        }
        
        stage('Deploy') {
            steps {
                echo 'Deploying the application...'
                sh 'docker-compose up -d'
            }
        }
    }
}
