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
                echo 'Testing... '
                sh 'cd webapp && sudo docker run --rm -e SONAR_HOST_URL="http://3.83.3.228:9000" -e SONAR_LOGIN="sqp_75d5223ade22a3030cd32898da656723ff825052"  -v ".:/usr/src" sonarsource/sonar-scanner-cli -Dsonar.projectKey=lms'
             }
        }
        stage('Build') {
            steps {
                echo 'Building...'
                sh 'cd webapp && npm install && npm run build'
            }
        }
        stage('Release') {
            steps {
                 script {
                   echo 'Releasing...'
                   def packageJSON = readJSON file: 'webapp/package.json'
                   def packageJSONVersion = packageJSON.version
                   echo "${packageJSONVersion}"  
                   sh "zip webapp/dist-${packageJSONVersion}.zip -r webapp/dist"
                   sh "curl -v -u admin:Nexus@123 --upload-file webapp/dist-${packageJSONVersion}.zip http://3.83.3.228:8081/repository/LMS/"     
            }
               }         
           }
        }
        stage('Deploy') {
            steps {
                script {
                   echo 'deploying...'
                   def packageJSON = readJSON file: 'webapp/package.json'
                   def packageJSONVersion = packageJSON.version
                   echo "${packageJSONVersion}"  
                   sh "curl -u admin:Nexus@123 -X GET \'http://3.83.3.228:8081/repository/LMS/dist-${packageJSONVersion}.zip\' --output dist-'${packageJSONVersion}'.zip"
                   sh 'sudo rm -rf /var/www/html/*'
                   sh "sudo unzip -o dist-'${packageJSONVersion}'.zip"
                   sh "sudo cp -r webapp/dist/* /var/www/html"
                }
           }
        }
    }
}

