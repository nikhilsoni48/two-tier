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
                    credentialsId: 'jenkins-master',
                    usernameVariable: 'DOCKER_USER',
                    passwordVariable: 'DOCKER_PASS'
                )]){
                    docker login -u $DOCKER_USER -p $DOCKER_PASS
                    docker tag two-tier-flask-app:latest nikhilsoni48/two-tier-flask-app:latest
                    docker push nikhilsoni48/two-tier-flask-app:latest
                }
            }
        }

        stage("deploy"){
            docker compose up -d --build flask-app -d
        }
    }
}
