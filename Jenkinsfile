pipeline {
    agent any

    tools {
        maven 'maven-3.8.6' // Make sure this matches the Maven version configured in Jenkins
    }

    environment {
        REMOTE_USER = 'ubuntu'
        REMOTE_HOST = '3.110.124.133'              // Change this to your Tomcat server IP
        REMOTE_PATH = '/home/ubuntu/apache-tomcat-9.0.100/webapps'
        SSH_KEY = '/var/lib/jenkins/.ssh/ubuntu.pem' // Update if your key has a different name/path
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
