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
                sh 'mvn test'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
            }
        }
    }
}
