
pipeline {
    agent any

    tools {
        maven 'maven-3.9.9' // Make sure this matches what's configured in Jenkins > Global Tools
    }

    environment {
        REMOTE_USER = 'ubuntu'
        REMOTE_HOST = '3.110.124.133'
        REMOTE_PATH = '/home/ubuntu/apache-tomcat-9.0.100/webapps'
        SSH_KEY = '/var/lib/jenkins/.ssh/tomcat-key.pem'
    }

    stages {
        stage('Checkout Code') {
            steps {
                git url: 'https://github.com/govindprasad7795/Petclinic-Real.git', branch: 'main'
            }
        }

        stage('Build WAR') {
            steps {
                withEnv(["PATH+MAVEN=${tool 'maven-3.8.6'}/bin"]) {
                    sh 'mvn clean package'
                }
            }
        }

        stage('Deploy WAR to Remote Tomcat') {
            steps {
                sh '''
                    echo "Copying WAR file to remote server..."
                    scp -i $SSH_KEY target/petclinic.war $REMOTE_USER@$REMOTE_HOST:$REMOTE_PATH/
                '''
            }
        }
    }

    post {
        success {
            echo '✅ Deployment successful!'
        }
        failure {
            echo '❌ Deployment failed!'
        }
    }
}
