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
             echo 'Setup is started'
                rtServer (
                    id: "springbootopenshift",
                    url: 'http://localhost:8082/artifactory',
                    username: 'admin',
                    password: 'Vipin@95',
                    timeout: 300
                )
                echo 'Setup is done'
             }
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
