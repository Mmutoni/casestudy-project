pipeline{
    agent {
        label 'ansible-agent'
    }
    stages{
        stage("check working directory"){
            steps{
                sh 'pwd'
                sh 'ls'
            }
        }
        stage('create a zipfile'){
            steps{
                sh ' wget https://github.com/Mmutoni/casestudy-project.git/archive/refs/heads/main.zip'

            }
        }
    }
}
