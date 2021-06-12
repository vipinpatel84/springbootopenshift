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
        stage ('Artifactory configuration') {
            
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

                rtMavenDeployer (
                    id: "springbootopenshift",
                    serverId: "springbootopenshift",
                    releaseRepo: 'http://localhost:8082/artifactory/springbootopenshift',
                    snapshotRepo: 'http://localhost:8082/artifactory/springbootopenshift'
                )

                rtMavenResolver (
                    id: "springbootopenshift",
                    serverId: "springbootopenshift",
                    releaseRepo: 'http://localhost:8082/artifactory/springbootopenshift',
                    snapshotRepo: 'http://localhost:8082/artifactory/springbootopenshift'
                )
            }
        }

        stage ('Exec Maven') {
            steps {
                rtMavenRun (
                    tool: 'maven', // Tool name from Jenkins configuration
                    pom: 'pom.xml',
                    goals: 'clean install',
                    deployerId: "MAVEN_DEPLOYER",
                    resolverId: "MAVEN_RESOLVER"
                )
            }
        }

        stage ('Publish build info') {
            steps {
                rtPublishBuildInfo (
                    serverId: "springbootopenshift"
                )
            }
        }
    }
}
