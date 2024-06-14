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
    }
}
