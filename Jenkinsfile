pipeline {
    agent any

    environment {
        REMOTE_HOST = '3.110.124.133'
        REMOTE_PATH = '/home/ubuntu/apache-tomcat-9.0.100/webapps'
    }

    stages {
        stage('Deploy') {
            steps {
                sshagent (credentials: ['tomcat-ssh-key']) {
                    sh """
                    scp -o StrictHostKeyChecking=no target/*.war ubuntu@${REMOTE_HOST}:${REMOTE_PATH}
                    """
                }
            }
        }
    }
}

