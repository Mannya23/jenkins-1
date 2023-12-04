pipeline {
    agent any

    environment {
        EKS_CLUSTER_NAME = "eksdemo"
        AWS_REGION = "us-east-1"
    }

    stages {
        stage('Build Maven') {
            steps {
                sh 'pwd'
                sh 'mvn clean install package'
            }
        }
    stage('Copy Artifacts') {
            steps {
                sh 'pwd'
                sh 'cp -r target/*.jar docker'
            }
        }
    stage('Unit Tests') {
            steps {
                sh 'mvn test'
            }
        }

    stage('Build Docker Image') {
            steps {
                script {
                    def customImage = docker.build("mrunalkhose/petclinic:${env.BUILD_NUMBER}", "./docker")
                    docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
                        customImage.push()
                    }
                }
            }
        }
    stage('Deploy to EKS') {
            steps {
                withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', accessKeyVariable: 'AKIA4NYBRLJXI32MPEAY', credentialsId: 'kubeconfig', secretKeyVariable: 'A76yBfokeWsrqD7RYTXF8NQmwa7HWxETaiUNDt/wG']]) {
                    withKubeConfig([credentialsId: 'kubeconfig']) {
                        sh 'pwd'
                        sh 'cp -R helm/* .'
                        sh 'ls -ltrh'
                        sh "pwd"

                        script {
                            sh "kubectl config use-context ${eksdemo}"
                            sh "/usr/local/bin/helm upgrade --install petclinic-app petclinic --set image.repository=mrunalkhose/petclinic --set image.tag=${BUILD_NUMBER}"
                        }
                    }
                }
            }
        }
    }
}