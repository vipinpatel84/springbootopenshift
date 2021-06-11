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
                   bat 'mvn clean install'
                }
                 echo 'Building. done'
            }
        }
        stage('Test') {
            steps {
                echo 'Testing..'
                withMaven(){
                   bat 'mvn test'
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
