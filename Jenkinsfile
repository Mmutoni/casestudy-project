/*pipeline{
   
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
        stage("deliver playbooks on /home/ec2-user/ansible"){
            steps{
                sh 'mkdir -p /home/ec2-user/ansible'
                sh 'cp -f /home/ec2-user/jenkins/workspace/ansible-master/main.zip /home/ec2-user/ansible'
                sh '''
                cd /home/ec2-user/ansible
                unzip -o main.zip
                rm -f main.zip
                cp -rf casestudy-project-main/* .
                rm -rf casestudy-project-main/
                '''
            }
        }
        stage('check working node connectivity'){
            steps{
                sh 'ansible all -m ping'
            }
        }
         stage("check test.yml"){
            steps{
                sh '''
                cd /home/ec2-user/ansible
                ansible-playbook test.yml --syntax-check
                '''
            }
        }
        stage("run playbook test.yml"){
            steps{
                sh 'ansible-playbook test.yml'
            }
        }
    }
}

*/
pipeline{
    agent any

    stages{
        stage('zip file'){
            steps{
                sh 'rm -rf *.zip || echo ""'
                sh 'zip -r ansible-${BUILD_ID}.zip * --exclude Jenkinsfile'
                
            }
        }
        stage('upload artifact to jfrog'){
            steps{
                sh 'curl -uadmin:AP8gcgmmset5jeYChTJYDN6XmDd -T \
                ansible-${BUILD_ID}.zip "http://http://54.147.142.41/:8081/artifactory/ansible-playbook/ansible-${BUILD_ID}.zip"'
            }
        }
        stage('publish to ansible server'){
            steps{
                sshPublisher(publishers:\
                    [sshPublisherDesc(configName: 'ansibleserver',\
                    transfers: [sshTransfer(cleanRemote: false, excludes: '', execCommand: 'unzip -o ansible-${BUILD_ID}.zip; rm -rf ansible-${BUILD_ID}.zip', \
                    execTimeout: 1200000, flatten: false, makeEmptyDirs: false, \
                    noDefaultExcludes: false, patternSeparator: '[, ]+', \
                    remoteDirectory: '.', \
                    remoteDirectorySDF: false, removePrefix: '', sourceFiles: 'ansible-${BUILD_ID}.zip')], \
                usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: false)])
            }
        }
    }
}