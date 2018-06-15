pipeline {
    agent any

     stage('SonarQube analysis') {
    // requires SonarQube Scanner 2.8+
    def scannerHome = '/var/jenkins_home/sonar-scanner';
    withSonarQubeEnv('sonarqube209') {
      sh "${scannerHome}/bin/sonar-scanner"
    }
  }
    
    stages {
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
