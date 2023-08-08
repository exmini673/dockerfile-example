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
        stage('Docker Image Push') {
            steps {
                script {
                    // Docker hub 에 로그인 하기 위해 사용
                    docker.withRegistry('https://index.docker.io/v1/', 'docker-hub') {
                        def httpd_img = docker.image('hiwill41/httpd')
                        def nginx_img = docker.image('hiwill41/nginx')
                        def loadbalancer_img = docker.image('hiwill41/loadbalancer')
                        
                        httpd_img.push('latest')
                        nginx_img.push('latest')
                        loadbalancer_img.push('latest')
                        
                        httpd_img.push('2.5')
                        nginx_img.push('2.5')
                        loadbalancer_img.push('2.5')
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
