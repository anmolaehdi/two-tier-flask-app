pipeline{
    
    agent { label "dev"};
    
    stages{
        stage ("code"){
            steps{
                git branch: 'master', url: 'https://github.com/anmolaehdi/two-tier-flask-app.git'
            }
        }
        stage ("Build"){
            steps{
                sh 'docker build -t two-tier-flask-app:latest .'
            }
        }
        stage ("Test"){
            steps{
                echo "Yaha par testing hogi"
            }
        }
        stage ("image sent to Dockerhub"){
            steps{
                withCredentials([usernamePassword(
                    credentialsId: "DockerHubCreds",
                    passwordVariable: "DockerHubPass",
                    usernameVariable: "DockerHubUser")]){
                        sh "docker login -u ${env.DockerHubUser} -p ${env.DockerHubPass}"
                        sh "docker image tag two-tier-flask-app:latest ${env.DockerHubUser}/two-tier-flask-app:latest"
                        sh "docker push ${env.DockerHubUser}/two-tier-flask-app:latest"
                    }
            }
        }
        stage ("Deploy"){
            steps{
                sh "docker compose up -d"
            }
        }
    }
}
