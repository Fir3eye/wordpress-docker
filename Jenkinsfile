pipeline{
    agent any

    stages{
        stage("Clean WorkSpace"){
            steps {
                cleanWs()
            }
        }
        stage("Checkout SCM"){
            steps {
                git branch: 'main', credentialsId: 'github', url: 'https://github.com/Fir3eye/wordpress-docker.git'
            }
        }
        stage("Build Docker Image"){
            steps{
                script {
                    docker.withRegistry('',DOCKER_PASS) {
                        sh "docker-compose up -d "
                        sh "docker tag wordpress:latest dockt35t/wordpress:latest"
                        sh "docker tag mysql:5.7 dockt35t/mysql:5.7"
                    }
                }
            }
        }
        stage("Push Docker Image"){
            steps{
                script {
                    docker.withRegistry('',DOCKER_PASS){
                        sh "docker push dockt35t/mysql:5.7"
                        sh "docker push dockt35t/wordpress:latest"
                    }
                }
            }
        } 
        stage ('Deploy to Container') {
            steps {
                sh 'docker run -d --name pet1 -p 808:8080 dockt35t/wordpress:latest'
            }
        }
    }
}
