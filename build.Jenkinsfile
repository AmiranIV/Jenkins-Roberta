pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                script {
                    withCredentials([usernamePassword(credentialsId: 'dockerLogin', usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD')]) {
                        sh '''
                            docker login -u $DOCKER_USERNAME -p $DOCKER_PASSWORD
                            docker build -t roberta-build-test:v1.0 .
                            docker tag roberta-build-test:v1.0 amiraniv/roberta-build-test:v1.1
                            docker push amiraniv/roberta-build-test:v1.1
                        '''
                    }
                }
            }
        }

        stage('Trigger Deploy') {
            steps {
                build job: 'Roberta-Deploy', wait: false, parameters: [
                    string(name: 'ROBERTA_IMAGE_URL', value: 'amiraniv/roberta-build-test:v1.1')
                ]
            }
        }
    }
}
