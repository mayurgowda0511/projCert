pipeline {
    agent any

    stages {
        stage('Clone Code') {
            steps {
               git credentialsId: 'github', url: 'https://github.com/mayurgowda0511/projCert.git'
               git branch: 'master', url: 'https://github.com/mayurgowda0511/projCert.git'
            }
        }
        //stage('Docker Build'){
        //    steps{
        //        sh "docker build . -t mayurgowda0511/my-php-website"
        //    }
        //}
        stage('DockerHub Push'){
            steps{
                script {
                    // Use Docker Hub credentials from Jenkins credentials store
                    withCredentials([usernamePassword(credentialsId: 'docker-hub-creds', usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD')]) {
                        sh "echo ${DOCKER_PASSWORD} | docker login -u ${DOCKER_USERNAME} --password-stdin"
                        sh "docker build -t mayurgowda0511/my-php-website ."
                        sh "docker push mayurgowda0511/my-php-website"
                    }
                }
                //withCredentials([string(credentialsId: 'docker-hub', variable: 'dockerPwd')]) {
                  //    sh "docker login -u mayurgowda0511 -p ${dockerPwd}"
                // }
                
                // sh "docker push mayurgowda0511/my-php-website"
            }
        }
         stage('Install docker and its dependencies and run contianer') {
            steps {
               ansiblePlaybook credentialsId: 'test-agent', installation: 'ansible', inventory: 'servers.inv', playbook: 'deployment-docker.yml'
            }
        }
    }
}
