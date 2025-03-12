pipeline{
    agent any
    tools{
        maven 'maven 3.8.6'
    }
    stages {
        stage('mvn build'){
            steps{
                sh 'mvn clean package'
            }
        }
        stage('Copy WAR File') {
            steps {
                sh 'cp target/petclinic.war /opt/apache-tomcat-9.0.102/webapps/'
            }
        }
        stage("Deploy To Tomcat"){
            steps{
                deploy adapters: [tomcat9(credentialsId: 'tomcat_username_password', path: '', url: 'http://3.110.124.133:8080/')], contextPath: null, war: '**/*.war'
            }
        }   
    }   
}

