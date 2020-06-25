pipeline {
    agent none
    stages {
        stage('Build jib image') {
            agent {
                docker {
                    image 'maven:3-jdk-11'
                    
                }
                
            }
            steps {
                git 'https://github.com/anunyavas/jenkins-pipeline.git'
                sh 'cd boxfuse-sample-java-war-hello && mvn package && mvn compile jib:build -DsendCredentialsOverHttp=true'
                
            }
            
        }
        stage('deploy image') {
            agent any
            steps {
            sh '''ssh -i /var/lib/tomcat8/id_rsa root@vm2 << EOF
            docker run -d -p 8080:8080 84.201.176.42:8082/appimage:latest
EOF'''
            }
                
          
        }
    }
}    
