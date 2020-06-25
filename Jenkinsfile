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
        sh 'cd jenkins-pipeline/boxfuse-sample-java-war-hello && mvn package && mvn compile jib:build -DsendCredentialsOverHttp=true'
      }
    }



    stage('Run docker on devbe-srv01') {
      steps {
        sh 'ssh-keyscan -H devbe-srv01 >> ~/.ssh/known_hosts'
        sh '''ssh jenkins@devbe-srv01 << EOF
	sudo docker pull devcvs-srv01:5000/shop2-backend/gateway-api:2-staging
	cd /etc/shop/docker
	sudo docker-compose up -d
EOF'''
      }
    }
  }
