pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                script {
                    sh '''
                        docker login 
                        docker build -t roberta-build-test:v1.0 .
                        docker tag roberta-build-test:v1.0 amiraniv/roberta-build-test:v1.1
                        docker push
                    '''
                }
            }
        }
    }
}

