pipeline {
    agent any
    stages {
        stage ('Clone') {
            steps {
                git branch: 'dev-v1', url: "https://github.com/vipinpatel84/springbootopenshift.git"
            }
        }
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
