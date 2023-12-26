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
                        sh "docker-compose up -d "
                        sh "docker tag wordpress:latest dockt35t/wordpress:latest"
                        sh "docker tag mysql:5.7 dockt35t/mysql:5.7"
                }
            }
        }
    }
}
