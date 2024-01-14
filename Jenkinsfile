pipeline {
    agent any

    stages {
        stage('Clone Code') {
            steps {
               git credentialsId: 'github', url: 'https://github.com/mayurgowda0511/projCert.git'
               git branch: 'master', url: 'https://github.com/mayurgowda0511/projCert.git'
            }
        }
       
        stage('DockerHub Push'){
            steps{
                script {
                    
                    withCredentials([usernamePassword(credentialsId: 'docker-hub-creds', usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD')]) {
                        sh "echo ${DOCKER_PASSWORD} | docker login -u ${DOCKER_USERNAME} --password-stdin"
                        sh "docker build -t mayurgowda0511/my-php-website ."
                        sh "docker push mayurgowda0511/my-php-website"
                    }
                }
              
            }
        }
         stage('Deploy Docker image in the server') {
            steps {
               // ansiblePlaybook credentialsId: 'test-agent', installation: 'ansible', inventory: 'servers.inv', playbook: 'deployment-docker.yml'
               sh "docker run -name myimage -d -P mayurgowda0511/my-php-website"
            }
        }
    }
}
