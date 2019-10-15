pipeline {
    agent any

    stages {
        stage("Deploy"){
            steps {
                echo "Going to deploy"
        
                sh """
                wget https://storage.googleapis.com/kubernetes-release/release/\$(wget https://storage.googleapis.com/kubernetes-release/release/stable.txt -O-)/bin/linux/amd64/kubectl -O ./kubectl
                chmod +x ./kubectl
                export PATH=\$PATH:\$(pwd)
                """
                withKubeConfig([
                    credentialsId: 'JENKINS_K8S_TOKEN', 
                    serverUrl: 'https://147.75.100.131:6443', 
                    namespace: "dev"]) {
                        sh """
                        ./kubectl apply -f nginx-deploy.yaml
                        """
                    }
                }

            }
        }

}