pipeline {
    agent { label 'jdk11-mvn3.8.4' }
    triggers { 
        cron('45 23 * * 1-5')
        pollSCM('*/5 * * * *')
    }
    stages {
        stage('scm') {
            steps {
               
                git url: 'https://github.com/GitPracticeRepo/spring-petclinic.git', branch: 'main'
            }
        }
        stage('build') {
            steps {
                withSonarQubeEnv(installationName: 'SONAR_9.2.1', envOnly: true, credentialsId: 'SONAR_TOKEN') {
                    sh "/usr/local/apache-maven-3.8.4/bin/mvn clean package sonar:sonar"
                    timeout(time: 1, unit: 'HOURS') {
                        waitForQualityGate abortPipeline: true
                    }
					
                    
                    
                }
                
            }
        }
        
    }
    
}
