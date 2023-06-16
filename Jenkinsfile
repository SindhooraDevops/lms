pipeline {
    agent any 
    stages {
        stage('Test') { 
            steps {
                echo "Testing..."
                sh 'cd webapp && sudo docker run --rm -e SONAR_HOST_URL="http://54.86.230.71:9000"-e SONAR_LOGIN="sqp_5b9883edd158fa33b89f3744317b7a59abfe8b7f" -v ".:/usr/src" sonarsource/sonar-scanner-cli -Dsonar.projectkey=LMS'          }
        }
        stage('Build') { 
            steps {
                echo "building..." 
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