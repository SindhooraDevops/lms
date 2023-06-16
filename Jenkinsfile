pipeline {
    agent any 
    stages {
        stage('Test') { 
            steps {
                echo "Testing..."
                sh 'cd webapp && sudo docker run --rm -e SONAR_HOST_URL="http://54.86.230.71:9000"-e SONAR_LOGIN="sqp_01b8b8948f19933972b89220645ab4246ed8b2d1" -v ".:/usr/src" sonarsource/sonar-scanner-cli -Dsonar.projectkey=lms-project'          }
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