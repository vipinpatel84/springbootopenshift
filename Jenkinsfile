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
                   sh 'mvn clean install'
                }
                 echo 'Building. done'
            }
        }
        stage('Test') {
            steps {
                echo 'Testing..'
                withMaven(){
                   sh 'mvn test'
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
