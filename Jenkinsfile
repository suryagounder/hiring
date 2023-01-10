pipeline {
    agent any

    stages {
        stage('git checkout') {
            steps {
               git branch: 'main', credentialsId: 'git-ci cd', url: 'https://github.com/suryagounder/hiring'
            }
        }
        
        stage('maven build') {
            steps {
               sh "mvn clean package"
            }
        }

        stage('tomcat deploy') {
            steps {
              sshagent(['tomcat-credss']) {
                 sh "scp -o StrictHostKeyChecking=no target/*.war ec2-user@52.196.142./opt/tomcat9/webapps"
                 sh "sshec2-user@52.196.142 /opt/tomcat9/bin/shutdown.sh"
                 sh "sshec2-user@52.196.142 /opt/tomcat9/bin/startup.sh"
                }
            }
        }
    }   
} 
