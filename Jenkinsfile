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
                sh 'cd webapp && sudo docker run --rm -e SONAR_HOST_URL="http://3.83.3.228:9000" -e SONAR_LOGIN="sqp_75d5223ade22a3030cd32898da656723ff825052"  -v ".:/usr/src" sonarsource/sonar-scanner-cli -Dsonar.projectKey=lms'
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

