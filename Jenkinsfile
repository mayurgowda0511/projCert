pipeline {
    agent any

    stages {
        stage('Clone Code') {
            steps {
               git credentialsId: 'github', url: 'https://github.com/mayurgowda0511/projCert.git'
               git branch: 'master', url: 'https://github.com/mayurgowda0511/projCert.git'
            }
        }
        stage('Docker Build'){
            steps{
                sh "docker build . -t mayurgowda0511/my-php-website"
            }
        }
        stage('DockerHub Push'){
            steps{
                
                withCredentials([string(credentialsId: 'docker-hub', variable: 'dockerPwd')]) {
                      sh "docker login -u mayurgowda0511 -p ${dockerPwd}"
                }
                
                sh "docker push mayurgowda0511/my-php-website"
            }
        }
         stage('Install docker and its dependencies and run contianer') {
            steps {
              // ansiblePlaybook credentialsId: 'test-agent', installation: 'ansible', inventory: 'servers.inv', playbook: 'deployment-docker.yml'
            }
        }
    }
}
