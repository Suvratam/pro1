pipeline {
    agent any
    stages{
        stage('build project'){
            steps{
                git url:'https://github.com/Suvratam/pro1.git', branch: "master"
                sh 'mvn clean package'
              
            }
        }
        stage('Build docker image'){
            steps{
                script{
                    sh 'docker build -t suvratam/staragileprojectfinance:v1 .'
                    sh 'docker images'
                }
            }
        }
        stage('Docker Login & Push') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-pwd', usernameVariable: 'USER', passwordVariable: 'PASS')]) {
                    sh 'echo $PASS | docker login -u $USER --password-stdin'
                    sh "docker push suvratam/staragileprojectfinance:v1"
                }
            }
        }
         
        
     stage('Deploy') {
            steps {
                sh 'sudo docker run -itd --name My-first-containe21211 -p 8083:8081 suvratam/staragileprojectfinance:v1'
                  
                }
            }
        
    }
}
