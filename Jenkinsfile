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
        stage('aws deployment'){
          steps{
          deploy adapters: [tomcat9(credentialsId: 'tomcatCredentials', path: '', url: 'https://3.15.0.139:8088')], contextPath: 'newAws', war: 'war'
        }
        }
    }
}
