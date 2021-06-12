pipeline {
    agent any
      options {
      timeout(time: 10, unit: 'MINUTES') 
    }
    stages {
        stage('Build') {
            steps {
                echo 'Building..'           
                withMaver(){
                   bat 'mvnw clean install'
                }
                 echo 'Building. done'
            }
        }
        stage('Test') {
            steps {
                echo 'Testing..'
                withMaven(){
                   sh 'mvnw test'
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
