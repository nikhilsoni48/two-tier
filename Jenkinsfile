pipeline{
    agent {
        label 'Agent'
    }

    stages{
        stage('code copy'){
            steps{
                git branch: 'master',
                    url: 'https://github.com/nikhilsoni48/two-tier.git'
            }
        }
        stage("build"){
            steps{
                sh "docker build -t two-tier-flask-app ."
            }
        }

        stage("test"){
            steps{
                echo "devloper test"
            }
        }

        stage("push to docekr hub"){
            steps{
                withCredentials([usernamePassword(
                    credentialsId: 'DockerHubCreds',
                    usernameVariable: 'DOCKER_USER',
                    passwordVariable: 'DOCKER_PASS'
                )]){
                    
                    sh "docker login -u ${env.DOCKER_USER} -p ${env.DOCKER_PASS}"
                    sh "docker image tag two-tier-flask-app ${env.DOCKER_USER}/two-tier-flask-app"
                    sh "docker push ${env.DOCKER_USER}/two-tier-flask-app"
                }
            }
        }

        stage("deploy"){
            steps{
                
                sh "docker compose up -d --build"
            }
        }
    }
}
