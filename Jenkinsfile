pipeline{
    
    agent { label "Agent"};
    
    stages{
        stage("Code Clone"){
            steps{
               script{
                   git url: 'https://github.com/nikhilsoni48/two-tier.git', branch: 'master'
               }
            }
        }

       stages {
    stage('Debug') {
        steps {
            sh '''
                whoami
                id
                groups
                docker ps
            '''
        }
    }

        
        stage("Build"){
            steps{
                sh "docker build -t two-tier-flask-app ."
            }
            
        }
        
        stage("Test"){
            steps{
                echo "Developer / Tester tests likh ke dega..."
            }
            
        }
        stage("Push to Docker Hub"){
            steps{
                script{
                    docker_push("dockerHubCreds","two-tier-flask-app")
                }  
            }
        }
        stage("Deploy"){
            steps{
                sh "docker compose up -d --build flask-app"
            }
        }
    }
}
