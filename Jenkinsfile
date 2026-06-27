pipeline{
    agent any

    stages{
        stage('build'){
            steps
           { 
            sh "docker build -t marwanmw/kube-client -f client/dockerfile client"
            sh "docker build -t marwanmw/kube-server -f server/dockerfile server"
            sh "docker build -t marwanmw/kube-worker -f worker/dockerfile worker"
            sh "docker build -t marwanmw/kube-nginx -f nginx/dockerfile nginx"
            }
        }
        stage('docker login'){
            steps{
            withCredentials([usernamePassword(credentialsId: 'docker-hub-credentials', passwordVariable: 'PASS', usernameVariable: 'USER')]) {
                sh "echo $PASS | docker login -u $USER --password-stdin"
            }
            }
        }
        stage('push'){
            steps
           { 
            sh "docker push marwanmw/kube-client"
            sh "docker push marwanmw/kube-server"
            sh "docker push marwanmw/kube-worker"
            sh "docker push marwanmw/kube-nginx"
            }
        }
    }
}