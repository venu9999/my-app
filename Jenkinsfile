pipeline{
    agent any
    stages{
    stage('Git checkout'){
            steps {
                script 
                {
                   git credentialsId: 'git-credentials', url: 'https://github.com/venu9999/my-app.git'
                }
           }
        }

        stage('Maven Build'){
            steps {
                script {

                    sh "mvn clean package"
                }
            }
        }
        stage('Docker build'){
    steps{
            script{
                    docker.withRegistry('https://651188399649.dkr.ecr.ap-southeast-2.amazonaws.com/', 'ecr:ap-southeast-2:demo-ecr-credentials') {
                    sh "docker build -t 651188399649.dkr.ecr.ap-southeast-2.amazonaws.com/catalog-demo:latest_${env.BUILD_ID} ."
                    }
                }
            }
        }
        stage('Docker push')
        {
            steps {
                script{
                    docker.withRegistry('https://651188399649.dkr.ecr.ap-southeast-2.amazonaws.com', 'ecr:ap-southeast-2:demo-ecr-credentials') {
                    sh "docker push 651188399649.dkr.ecr.ap-southeast-2.amazonaws.com/catalog-demo:latest_${env.BUILD_ID}"
                    }
                    sh "docker rmi 651188399649.dkr.ecr.ap-southeast-2.amazonaws.com/catalog-demo:latest_${env.BUILD_ID}"
                    }
            }
        }

    } 

}    
