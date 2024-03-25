pipeline {
    agent any
    environment { 
    DOCKER_ID = "dstdockerhub"
    DOCKER_IMAGE = "datascientestapi"
    DOCKER_TAG = "v.${BUILD_ID}.0" 
    }
    stages {
        stage('Building') {
            steps {
                  sh 'pip install -r requirements.txt'
            }
        }
        stage('Testing') {
            steps {
                  sh 'python3 -m unittest'
            }
        }
        stage('Deploying') {
            steps {
                script {
                  sh '''
                      docker rm -f jenkins
                      docker build -t $DOCKER_ID/$DOCKER_IMAGE:$DOCKER_TAG .
                      docker run -d -p 5000:5000 --name jenkins $DOCKER_ID/$DOCKER_IMAGE:$DOCKER_TAG
                  '''
                }
            }
        }
    }
}
