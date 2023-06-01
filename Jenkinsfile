
pipeline {
    agent any

    stages {
        stage('Clean Workspace') {
            steps {
                cleanWs()
            }
        }

        stage('checkout_code') {
            steps {
                checkout scmGit(
                    branches: [[name: '*/main']],
                    extensions: [],
                    userRemoteConfigs: [[credentialsId: 'omer', url: 'https://github.com/omerweiner/react-java0mysql.git']]
                )
            }
        }



        stage('Build - Code') {
            steps {
                echo "Building code now"
                sh 'echo "1111" | sudo -S /bin/bash'
                sh 'docker-compose up -d'
            }
        }

        stage('Test') {
            steps {
                echo "Testing code now"
                sh 'docker ps -a'
                sh 'IP=$(curl -s http://checkip.amazonaws.com)'
                sh 'curl -s "http://$IP:3000"' //curling the public ip on port 3000 to check if pod online 
            }
        }

        stage('Package-code') {
            steps {
                echo "Package code"
                sh 'tar -czvf package-$BUILD_ID.tar.gz *'
                archive '*.tar.gz'
                 
            }
        }
                    stage('artifactory  ') {
            steps {
                
            sh 'docker tag module6_frontend omer5800devops.jfrog.io/docker-trial/react-java0mysql-frontend-1:$BUILD_ID'
            sh 'docker tag module6_backend omer5800devops.jfrog.io/docker-trial/react-java0mysql-backend-1:$BUILD_ID'
            sh 'docker tag module6_mariaDB omer5800devops.jfrog.io/docker-trial/react-java0mysql-mariaDB-1:$BUILD_ID'


                 
            }
        }
    }
}
