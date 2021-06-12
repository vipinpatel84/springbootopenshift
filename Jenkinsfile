pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                echo 'Build Started'
                withMaven(){
                    bat 'mvn clean install'
                }
            }
        }
         stage('Push to Artifactory') {
            steps {
                echo ' Started '
                withMaven(){
                    bat 'mvn deploy -Dmaven.test.skip=true'
                }
                echo ' end '
            }
        }                      
                
    }
}
