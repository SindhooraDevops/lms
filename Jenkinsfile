pipeline {
    agent any 
    stages {
        stage('Test') { 
            steps {
                echo "Testing..."
                sh 'cd webapp && sudo docker run --rm -e SONAR_HOST_URL="http://54.86.230.71:9000"-e SONAR_LOGIN="sqp_b3409dc9035d67fd37429d6cb92feed2fdad013c" -v ".:/usr/src" sonarsource/sonar-scanner-cli -Dsonar.projectkey=lmsproject'        
            }
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