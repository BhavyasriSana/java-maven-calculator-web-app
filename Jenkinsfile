pipeline {
    agent any
    tools {
        maven "Maven"   
    }    
    stages {
        stage('Compile-Build-Test') {
            steps {
                sh 'mvn clean package'
            }
        }
        stage('SonarQube Analysis'){
            steps{
                withSonarQubeEnv('sonarqube'){
                    sh 'mvn sonar:sonar'
                }
            }
        }
         stage('Deployment to AWS'){
            steps{
            deploy adapters: [tomcat8(credentialsId: 'tomcatCredentials', path: '', url: 'http://3.15.0.139:8088/')], contextPath: 'new', onFailure: false, war: '**/target/*.war'
            }
        }
       
    }
}
