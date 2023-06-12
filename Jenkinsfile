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
                sh 'cd webapp && sudo docker container run --rm -e SONAR_HOST_URL="http://44.201.105.57:9000" -e SONAR_LOGIN="sqp_8205a139685881fd0d97cc07457d99b84b480ae0" -v ".:/usr/src" sonarsource/sonar-scanner-cli -Dsonar.projectKey=lms'
            }
        }
        stage('Release') {
            steps {
                echo 'Release Nexus'
                def packageJSON = readJSON file: 'webapp/package.json'
                def packageJSONVersion = packageJSON.version
                echo packageJSONVersion
                sh 'VERSION=${packageJSONVersion}_${BUILD_NUMBER}_${BRANCH_NAME} npm run build'
                sh 'zip webapp/dist-${package.JSON version}.zip -r webapp/dist'
                sh 'curl -v -u admin:Nexus@123* --upload-file webapp/dist-${package.JSON version}.zip http://44.201.105.57:8081/repository/lms/'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Release Nexus'
                sh 'rm -rf *.zip'
                sh 'cd webapp && zip dist-${BUILD_NUMBER}.zip -r dist'
                sh 'cd webapp && curl -v -u $admin:$Nexus@123 --upload-file dist-${BUILD_NUMBER}.zip http://3.95.245.19:8081/repository/lms/'
            }
        }
    }
}
}
