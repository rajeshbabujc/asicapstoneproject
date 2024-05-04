pipeline{
    agent any
    stages{
        stage('Build Maven'){
            steps{
                checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/rajeshbabujc/asicapstoneproject']])
                sh 'mvn clean install'
            }
        }
        stage('Build Docker Image'){
            steps{
                script{
                    sh 'docker build -t docrajesh123/asiinsuranceapp .'
                }
            }
        }
        stage('Push Docker Image to Dockerhub'){
            steps{
                script{
                    withCredentials([gitUsernamePassword(credentialsId: 'dockerhubpwd', gitToolName: 'Default')]) {
                    sh 'docker login -u docrajesh123 -p capstoneasi@132S'
                    sh 'docker push docrajesh123/asiinsuranceapp'
                    }
                }
            }
        }
        stage('Execute Ansible Playbook'){
            steps{
                    sh 'ansible-playbook ansible-playbook.yml'
            }
        }
    }
}
