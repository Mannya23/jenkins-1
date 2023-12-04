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
    }
}
        