pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building Cloudfuse code'
                sh 'yum install gcc make fuse-devel curl-devel libxml2-devel openssl-devel -y'
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
                sh 'sudo make install'
            }
        }
    }
}
