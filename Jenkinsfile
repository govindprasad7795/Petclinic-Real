pipeline{
    agent any
    tools{
        maven 'maven1'
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
                deploy adapters: [tomcat9(credentialsId: '25cb7e4c-4d6e-40ef-a83f-e645cf95bc11', path: '', url: 'http://44.204.71.136:8083/')], contextPath: null, war: '**/*.war'
            }
        }   
    }   
}

