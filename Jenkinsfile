pipeline {
    agent any
        environment {
            DOCKERHUB_CREDENTIALS = credentials('tomkatzav-dockerhub')
    }
    
    stages {

        stage('Build') { 
            steps {
                sh '''
                    echo building docker containers
                    export TAG=$BUILD_NUMBER
                    docker-compose up --build -d
                '''      
            }
	        post {
                failure {
                    echo 'Build failed :('
                    slackSend channel: '#devop-alerts', color: 'warning', message: 'Stage Build Fail'
                }
	        }
        }

        stage('Test') { 
            steps {
                sh '''
                    echo testing'
                    pytest ./tests/unit_test.py'
                    pytest ./tests/docker_image_test.py'
                '''
            }
	        post {
                failure {
                    echo 'Test failed :('
                    slackSend channel: '#devop-alerts', color: 'warning', message: 'Stage Test Fail'
                }
            }
        }

        stage('Login and Push Dockerhub') {
            steps {
                sh '''
                    echo Login to Dockerhub
                    echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin

                    echo Push to Dockerhub
                    docker push tomkatzav/weather:v-$BUILD_NUMBER
                '''
            }
            post {
                failure {
                    echo 'Login and Push Dockerhub failed :('
                    slackSend channel: '#devop-alerts', color: 'warning', message: 'Stage Login and Push Dockerhub Fail'
                }
            }
        }

        stage('Deploy') { 
            steps {
                sh '''
                    echo Deploy with docker daemon
                    export TAG=$BUILD_NUMBER
                    docker-compose -H tcp://$PRODUCTION_SERVER rm -fs
                    docker-compose -H tcp://$PRODUCTION_SERVER up --build -d
                ''' 
            }
            post {
                failure {
                    echo 'Deploy failed :('
                    slackSend channel: '#devop-alerts', color: 'warning', message: 'Stage Deploy Fail'
                }
            }
        }

        stage('Clean') { 
            steps {
                sh '''
                    echo clean
                    docker rm -f $(sudo docker ps -a -q)
                    docker rmi -f $(sudo docker images -q)
                    docker-compose rm -fs
                ''' 
            }
        }
    }

    post {
        always {
            sh 'echo logout from Dockerhub'
            sh 'docker logout' 
        }

	    success {
            slackSend channel: '#successful-build', color: 'good', message: 'Pipline Success'
        }
    }
}
