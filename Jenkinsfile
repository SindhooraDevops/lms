pipeline {
    agent any 
    stages {
        stage('Test') { 
            steps {
                echo "Testing..."
                sh 'cd webapp && sudo docker run --rm -e SONAR_HOST_URL="http://54.86.230.71:9000"-e SONAR_LOGIN="sqp_3a09bd390f4c25628ce132b9ff0a502b1b1567d9" -v ".:/usr/src" sonarsource/sonar-scanner-cli -Dsonar.projectkey=lmsproject'        
            }
        }
        stage('Build') { 
            steps {
                echo "building..." 
                sh 'cd webapp && npm install && npm run build'
            }
        }
        stage('Release') { 
            steps {
                echo "Releasing.."       
                    def packageJSON = readJSON file: 'webapp/package.json'
                    def packageJSONVersion = packageJSON.version
                    echo "${packageJSONVersion}"  
                    sh "zip webapp/dist-${packageJSONVersion}.zip -r webapp/dist"
                    sh "curl -v -u admin:Nexus@123 --upload-file webapp/dist-${packageJSONVersion}.zip http://54.86.230.71:8081/repository/LMS/"      
            }
        }
        stage('Deploy') { 
            steps {
                echo "deploying..." 
                def packageJSON = readJSON file: 'webapp/package.json'
                    def packageJSONVersion = packageJSON.version
                    echo "${packageJSONVersion}"  
                    sh "curl -u admin:Nexus@123 -X GET \'http://54.86.230.71:8081/repository/LMS/dist-${packageJSONVersion}.zip\' --output dist-'${packageJSONVersion}'.zip"
                    sh 'sudo rm -rf /var/www/html/*'
                    sh "sudo unzip -o dist-'${packageJSONVersion}'.zip"
                    sh "sudo cp -r webapp/dist/* /var/www/html"
            }
        }
    }
}