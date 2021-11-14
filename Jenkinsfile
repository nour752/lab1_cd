pipeline {
  agent any
    stages {
        stage('Pull') {
             steps{
                script{
                    checkout([$class: 'GitSCM', branches: [[name: '*/master']],
                        userRemoteConfigs: [[
                            url: 'https://github.com/nour752/lab1_cd']]])
                }
            }
        }
        stage('Install') {
             steps{
                script{
                    sh "sudo npm install"
                }
            }
        }
        stage('Build') {
             steps{
                script{
                    sh "sudo ansible-playbook ansible/build.yml -i ansible/inventory/host.yml"
                }
            }
        }
        stage('ng Build') {
             steps{
                script{
                    sh "sudo ng build"
                }
            }
        }
        stage('Docker') {
             steps{
                script{
                    sh "sudo ansible-playbook ansible/docker.yml -i ansible/inventory/host.yml"
                }
            }
        }
       stage('To DockerHub') {
             steps{
                script{
                    sh "ansible-playbook ansible/docker-registry.yml -i ansible/inventory/host.yml"
                }
            }
        }        
       }
      }
