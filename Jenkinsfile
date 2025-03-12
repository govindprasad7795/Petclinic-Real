pipeline {
    agent any

    environment {
        REMOTE_HOST = '3.110.124.133'
        REMOTE_PATH = '/home/ubuntu/apache-tomcat-9.0.100/webapps'
    }

    stages {
        stage('Build') {
            steps {
                echo 'Building project with Maven...'
                sh 'mvn clean package'
            }
        }

        stage('Deploy') {
            steps {
                echo "Deploying WAR to ${REMOTE_HOST}..."

                sshagent(['tomcat-ssh-key']) {
                    sh '''
                        echo "Transferring WAR file to remote server..."
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
