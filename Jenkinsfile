pipeline{
    agent { label 'dev-agent'}
    stages{
        stage('code cloned'){
            steps{
                script{
                    properties([pipelineTriggers([pollSCM('')])])
                }
                git url:'https://github.com/pulkitgupta18/node-todo-cicd.git',branch:'master'
            }
        }
        stage('Build and test'){
            steps{
                sh 'docker build . -t pulkit3245/node-to-app:latest'
            }
        }
        stage('login and push'){
            steps{
                echo "login in docke hub and pushing image into it"
                withCredentials([usernamePassword(credentialsId:'dockerhub',passwordVariable:'dockerhubpassword',usernameVariable:'dockerhubusername')]){
                sh "docker login -u ${env.dockerhubusername} -p ${env.dockerhubpassword}"
                sh "docker push pulkit3245/node-to-app:latest"
                }    
            }
    
        }
        stage('Deploying'){
            steps{
                sh 'docker-compose down && docker-compose up -d'
            }
        }
    }
}
