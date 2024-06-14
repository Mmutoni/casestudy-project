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
        stage('deploying artifact to jfrog'){
            steps{
                sh 'curl -uadmin:AP8gcgmmset5jeYChTJYDN6XmDd \
                 -T /home/ec2-user/jenkins/workspace/ansible-master/main.zip \
                  "http://52.87.222.247:8081/artifactory/ansible-playbook/playbook_${BUILD_ID}.zip"'
            }
        }
    }
}
