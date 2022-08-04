pipeline{
    agent { label 'linux'}

    stages {
        stage('Checkout Source') {
            steps {
                git branch: 'main', url: 'https://github.com/nhhoang27/helm_chart_CI_CD.git'
            }
        }

        stage('Build') {
            steps {
                sh 'docker build -t 172.16.10.109:5000/nodeapp:latest .'
            }
        }

        stage('Push') {
            steps {
                sh 'docker push 172.16.10.109:5000/nodeapp:latest'
            }
        }
        
        // stage('Deploying to k8s') {
        //     steps {
        //         script {
        //             kubernetesDeploy(configs: 'deploymentservice.yml', kubeconfigId: 'kubernetes')
        //         }
        //     }
        // }
        
        stage('Deploying with Helm Chart') {
            steps {
                script {
//                     sh "helm upgrade --install --token kubernetes example-project example-project "
                        helmDeploy(example-project, "kubernetes")
                }
            }
        }
    }
    
    // post {
    //     always {
    //         cleanWs()
    //     }
    // }
} 
