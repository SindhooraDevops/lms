pipeline {
    agent any
    environment {
        // More detail: 
        // https://jenkins.io/doc/book/pipeline/jenkinsfile/#usernames-and-passwords
        NEXUS_CRED = credentials('nexus')
          }

    stages {
        stage('Sonar analysis') {
            steps {
                echo 'Testing..'
                sh 'cd webapp && sudo docker run --rm -e SONAR_HOST_URL="http://34.227.112.54:9000" -e SONAR_LOGIN="sqp_6ac3830625d1b0db9518f1b212a4b748374ba00c"  -v ".:/usr/src" sonarsource/sonar-scanner-cli -Dsonar.projectKey=lms'
             }
        }
        stage('Build') {
            steps {
                echo 'Building..'
                sh 'cd webapp && npm install && npm run build'
            }
        }
        stage('Release') {
            steps {
                 script {
                    
               }
           }
        }
        stage('Deploy') {
            steps {
                script {
                    
                }
           }
        }
    }
}

