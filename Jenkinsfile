pipeline {
    agent any
    environment {
        // More detail: 
        // https://jenkins.io/doc/book/pipeline/jenkinsfile/#usernames-and-passwords
        NEXUS_CRED = credentials('nexus')
   }

    stages {
        stage('Build') {
            steps {
                echo 'Building..'
                sh 'cd webapp && npm install && npm run build'
            }
        }
        stage('Test') {
            steps {
                echo 'Testing..'
                sh 'cd webapp && sudo docker container run --rm -e SONAR_HOST_URL="http://34.227.112.54:9000" -e SONAR_LOGIN="sqp_6ac3830625d1b0db9518f1b212a4b748374ba00c" -v ".:/usr/src" sonarsource/sonar-scanner-cli -Dsonar.projectKey=lms'
            }
        }
        stage('Release') {
            steps {
                echo 'Release Nexus'
                def packageJSON = readJSON file: 'webapp/package.json'
                def packageJSONVersion = packageJSON.version
                echo '${packageJSONVersion}'
                sh 'zip webapp/dist-${packageJSONversion}.zip -r webapp/dist'
                sh 'curl -v -u admin:Nexus@123* --upload-file webapp/dist-${packageJSONversion}.zip http://34.227.112.54:8081/repository/lms/'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Release Nexus'
                def packageJSON = readJSON file: 'webapp/package.json'
                def packageJSONVersion = packageJSON.version
                echo '${packageJSONVersion}'
                sh 'curl -u admin:Nexus@123* -X GET http://34.227.112.54:8081/repository/LMS/dist -${packageJSONversion}.zip'--output dist -'${packageJSONVersion}'
                sh 'sudo rm -rf /var/www/html/*'
                sh 'sudo unzip -o dist -'${packageJSONversion}'.zip'
                sh 'sudo cp -r webapp/dist/* /var/www/html'
           }
        }
    }
}

