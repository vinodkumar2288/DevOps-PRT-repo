pipeline {
    agent none
    
    environment {
        DOCKERHUB_CREDENTIALS = credentials('')
    }
    
    stages {
        stage('Hello') {
            agent { labele 'KMaster' }
            steps {
                echo 'Hello World'
            }
        }
        
        stage('Git Checkout') {
            agent { label 'KMaster' }
            steps {
                git url: 'https://github.com/vinodkumar2288/DevOps-PRT-repo.git'
            }
        }
        
        stage('Docker Build & Push') {
            agent { label 'KMaster' }
            steps {
                sh '''
                docker build -t docker6767/image .
                echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --
                docker push docker6767/image
                '''
            }
        }
        
        stage('Kubernetes Deploy') {
            agent { label 'KMaster' }
            steps {
                sh '''
                kubectl apply -f deploy.yml
                kubectl apply -f svc.yml
                '''
            }
        }
    }
}
