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
        stage("delete old artifact if exist"){
            steps{
                sh 'rm -rf *.zip || echo ""'
            }
        }
        stage('create a zipfile'){
            steps{

         sh 'wget https://github.com/Mmutoni/casestudy-project/archive/refs/heads/main.zip'

            }
        }
    }
}
