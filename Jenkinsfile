pipeline {
    agent any
      options {
      timeout(time: 10, unit: 'MINUTES') 
    }
    stages {
        stage('Build') {
            steps {
                sh 'mvn clean install'
                echo 'Building..'
                echo 'Building..'
                echo 'Building..'
            }
        }
        stage('Test') {
            steps {
                echo 'Testing..'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
            }
        }
    }
}
