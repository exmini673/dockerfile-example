pipeline{
    agent any
    triggers {
        githubPush()
    }
    options {
        timestamps()
    }
    stages {
        stage('Github Clone & Checkout') {
            steps {
                git branch: 'main', // Corrected branch name
                    url: 'https://github.com/exmini673/dockerfile-example.git',
                    credentialsId: ''
            }
        }
        stage('Docker Build Apache') {
            steps {
                script {
                    docker.withRegistry('https://index.docker.io/v1/', 'docker-hub') {
                        docker.build('hiwill41/httpd', '--no-cache ./ubuntu_apache2') // Corrected image name and Dockerfile path
                    }
                }
            }
        }
        stage('Docker Build Nginx') {
            steps {
                script {
                    docker.withRegistry('https://index.docker.io/v1/', 'docker-hub') {
                        docker.build('hiwill41/nginx', '--no-cache ./ubuntu_nginx') // Corrected image name and Dockerfile path
                    }
                }
            }
        }
        stage('Docker Build Load Balancer') {
            steps {
                script {
                    docker.withRegistry('https://index.docker.io/v1/', 'docker-hub') {
                        docker.build('hiwill41/loadbalancer', '--no-cache ./ubuntu_nginx_loadbalancer') // Corrected image name and Dockerfile path
                    }
                }
            }
        }
    }
    post {
        cleanup {
            emailext subject: '$DEFAULT_SUBJECT', 
                     to: 'exmini673@gmail.com',
                     body: '$DEFAULT_CONTENT'
            cleanWs() // Workspace cleanup
        }
    }
}
