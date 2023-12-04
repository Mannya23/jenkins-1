pipeline {
    agent any

     environment {
        EKS_CLUSTER_NAME = "eksdemo"
        AWS_REGION = "us-east-1"
    }
    stages {
        stage('Debug') {
            steps {
                script {
                    echo "Access Key: ${env.AKIA4NYBRLJXI32MPEAY}"
                    echo "Secret Key: ${env.A76yBfokeWsrqD7RYTXF8NQmwa7HWxETaiUNDt_wG}"
                    echo "Credentials ID: ${env.credentialsId}"
                }
            }
        }         
    }  
}    