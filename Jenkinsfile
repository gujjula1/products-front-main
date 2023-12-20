pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                sh'''
                    echo "BuildinG docker image..."
                    docker build -t products-frontend:v1 .
                    docker tag products-frontend:v1 gujjula1/jenkins-products-frontend:v$BUILD_NUMBER
                '''
            }
        }
        stage('Push') {
            steps {
                sh'''
                    echo "Pushing docker image into Dockerhub..."
                    docker push gujjula1/jenkins-products-frontend:v$BUILD_NUMBER 
                '''
            }
        }
        stage('Deploy') {
            steps {
                sh'''
                    echo "Deploying into new server"
                    ssh ubuntu@13.235.238.103 docker service update --image gujjula1/jenkins-products-frontend:v$BUILD_NUMBER products_frontend
                '''
            }
    }
        
}
}



