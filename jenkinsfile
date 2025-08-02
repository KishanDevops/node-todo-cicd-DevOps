pipeline{
    agent any
    
    stages{
        stage('Code'){
            steps{
                echo "Code Colneing github repo"
                git url: 'https://github.com/kishan-37/node-todo-cicd.git', branch: 'master'
            }
        }
        stage('Build'){
            steps{
                echo "Build github repo"
                sh 'docker build . -t kishan60/node-todo-test:lastest'
            }
        }
        stage('push'){
            steps{
                echo "push github repo"
                withCredentials([usernamePassword(credentialsId: 'dockerHub', passwordVariable: 'dockerHubPassword', usernameVariable: 'dockerHubUser')]) {
                sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPassword}"
                sh 'docker push kishan60/node-todo-test:lastest'
                }
            }
        }
        stage('Deploy'){
            steps{
                echo "docker-compose"
                sh 'docker-compose down && docker-compose up -d'
            }
        }
    }
}
