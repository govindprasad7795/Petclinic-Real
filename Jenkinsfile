pipeline{
    agent any
    tools{
        maven 'maven1'
    }
    stages {
        stage('mvn build'){
            steps{
                sh 'mvn clean package'
                sh 'mv target/*.war target/Petclinic-Real'
            }
        }  
        
        stage("Deploy To Tomcat"){
            steps{
                deploy adapters: [tomcat9(credentialsId: '25cb7e4c-4d6e-40ef-a83f-e645cf95bc11', path: '', url: 'http://54.175.230.33:8083/')], contextPath: null, war: '**/*.war'
            }
        }   
    }   
}

