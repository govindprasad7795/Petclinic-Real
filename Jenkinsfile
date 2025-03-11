pipeline{
    agent any
    tools{
        maven 'maven1'
    }
    stages {
        stage('Checkout From Git'){
            steps{
                git branch: 'main', credentialsId: '3e65bdf0-de0a-46e1-97f1-0537122e72ba', url: 'https://github.com/Manjula-g475/Petclinic-Real.git'
            }
        }
        stage('mvn compile'){
            steps{
                sh 'mvn clean compile'
            }
        }
        stage('mvn test'){
            steps{
                sh 'mvn test'
            }
        }
        stage('mvn build'){
            steps{
                sh 'mvn clean install'
            }
        }  
        
        stage("Deploy To Tomcat"){
            steps{
                deploy adapters: [tomcat9(credentialsId: '25cb7e4c-4d6e-40ef-a83f-e645cf95bc11', path: '', url: 'http://54.175.230.33:8083/')], contextPath: null, war: '**/*.war'
            }
        }   
    }   
}

