pipeline {
    agent any
    stages{
        stage('git cloned'){
            steps{
                git url:'https://github.com/sami687/project/', branch: "master"
              
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
        
     stage('Deploy') {
            steps {
                     sh 'sudo docker run -itd --name My-first-containe2211 -p 8083:80 samiksha055/bankingandfinance:v1'

                }
            }
        }
    }
