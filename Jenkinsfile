pipeline {
    agent any
    stages{
        stage('build project'){
            steps{
                git url:'https://github.com/sami687/project/', branch: "master"
                 sh 'mvn clean package'
            }
        }
        stage('Build docker image'){
            steps{
                script{
                    sh 'docker build -t samiksha055/bankingandfinance:v1 .'
                    sh 'docker images'
                }
            }
        }
          stage('Docker login') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-pwd', passwordVariable: 'PASS', usernameVariable: 'USER')]) {
                    sh "echo $PASS | docker login -u $USER --password-stdin"
                    sh 'docker push samiksha055/bankingandfinance:v1'
                }
            }
        }
        
     stage('deploy on ansible') {
            ansiblePlaybook become: true, credentialsId: 'ansible', disableHostKeyChecking: true, installation: 'ansible', inventory: '/etc/ansible/hosts' , playbook: 'playbook.yml' vaultTempPath: "

                }
            }
        }
    }
