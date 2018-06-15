pipeline {
    agent any
    
    stages {
        
    stage('SonarQube analysis') {
    // requires SonarQube Scanner 2.8+
    steps {
    withSonarQubeEnv('sonarqube209') {
      sh "/var/jenkins_home/sonar-scanner/bin/sonar-scanner"
        }
    }
  }
        
        stage('Build') {
            steps {
                echo 'Building Cloudfuse code'
                sh 'apt-get install build-essential libcurl4-openssl-dev libxml2-dev libssl-dev libfuse-dev libjson-c-dev pkg-config -y'
                sh './configure'
                sh 'make'
            }
        }
        stage('Test') {
            steps {
                echo 'Testing..'
            }
        }
        stage('Deploy') {
            when {
              expression {
                currentBuild.result == null || currentBuild.result == 'SUCCESS' 
              }
            }
            steps {
                echo 'Deploying....'
                sh 'make install'
            }
        }
    }
}
