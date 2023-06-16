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
                echo "realising..." 
            }
        }
        stage('Deploy') { 
            steps {
                echo "deploying..." 
            }
        }
    }
}