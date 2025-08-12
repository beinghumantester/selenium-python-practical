pipeline {
    agent any

    stages {
        stage('Build pyTest') {
            steps {
                git branch: 'main', url: 'https://github.com/beinghumantester/selenium-python-practical.git'
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                    // Use bat if on Windows agent
                    bat 'docker build -t beinghumantester/selenium-python-practical .'
                }
            }
        }
      stage('Push Docker Image') {
    steps {
        script {
            withCredentials([string(credentialsId: 'dockerhub-pwd', variable: 'dockerhubpwd')]) {
                // For Windows agent, use bat; for Linux, use sh
                bat """
                docker login -u beinghumantester -p ${dockerhubpwd}
                docker push beinghumantester/selenium-python-practical
                """
            }
        }
    }
}

        stage('List files') {
            steps {
                bat 'dir'
            }
        }
        stage('Install dependencies') {
            steps {
                bat 'pip install -r requirements.txt'
            }
        }
        stage('Run Pytest') {
            steps {
                bat 'pytest'
            }
        }
    }
}
