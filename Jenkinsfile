pipeline {
    agent any
      options {
      timeout(time: 10, unit: 'MINUTES') 
    }
    stages {
        stage('Build') {
            steps {
                echo 'Building..'           
                withMaven(){
                   bat 'mvn -B -DskipTests clean package'
                }
                 echo 'Building. done'
            }
        }
        stage('Test') {
            steps {
                
                echo 'Testing..'
                steps {
           bat 'mvn test'
                    }
            post {
                always {
                    junit 'target/surefire-reports/*.xml'
                }
            }
                echo 'testing done .....'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
            }
        }
    }
}
