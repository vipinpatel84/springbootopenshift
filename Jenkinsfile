pipeline {
    agent any
    environment {
    ARTIFACTORY_CREDS = credentials('ARTIFACTORY_CRED')
        }
    stages {
        stage ('Clone') {
            steps {
                git branch: 'dev-v1', url: "https://github.com/vipinpatel84/springbootopenshift.git"
            }
         }
                
        stage ('Build') {
            steps {
                rtServer (
                    id: "artifactory",
                    url: "http://localhost:8081/artifactory",
                    credentialsId: 'ARTIFACTORY_CREDS',
                )

                rtMavenDeployer (
                    id: "MAVEN_DEPLOYER",
                    serverId: "artifactory",
                    releaseRepo: 'springbootopenshift',
                    snapshotRepo: 'springbootopenshift'
                )

                rtMavenResolver (
                    id: "MAVEN_RESOLVER",
                    serverId: "artifactory",
                    releaseRepo: "springbootopenshift",
                    snapshotRepo: "springbootopenshift"
                )
                
                rtMavenRun (
                    tool: 'maven_apache', // Tool name from Jenkins configuration
                    pom: 'pom.xml',
                    goals: 'clean install',
                    deployerId: "MAVEN_DEPLOYER",
                    resolverId: "MAVEN_RESOLVER"
                )
            }
        }

        stage ('Deploy') {
            steps {
                rtPublishBuildInfo (
                    serverId: "artifactory"
                )
            }
        }
    }
}
