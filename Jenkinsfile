pipeline {
    agent any

    environment {
        REMOTE_HOST = '3.110.124.133'
        REMOTE_PATH = '/home/ubuntu/apache-tomcat-9.0.100/webapps'
    }

    stages {
        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Deploy') {
            steps {
                sshagent(['tomcat-ssh-key']) {
                    sh '''
                        scp -o StrictHostKeyChecking=no target/*.war ubuntu@${REMOTE_HOST}:${REMOTE_PATH}
                    '''
                }
            }
        }
    }

    post {
        success {
            echo 'Build and deployment completed successfully.'
        }
        failure {
            echo 'Something went wrong during build or deployment.'
        }
    }
}

