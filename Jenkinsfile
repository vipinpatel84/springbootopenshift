pipeline {
    agent any
    stages {
        stage ('Clone') {
            steps {
                git branch: 'dev-v1', url: "https://github.com/vipinpatel84/springbootopenshift.git"
            }
        }

        stage ('Artifactory configuration') {
            steps {
                rtServer (
                    id: "artifactory",
                    url: "http://localhost:8081/artifactory",
                    username: 'admin',
                    password: 'Vipin@95',
                )

                rtMavenDeployer (
                    id: "maven_apache",
                    serverId: "artifactory",
                    releaseRepo: 'springbootopenshift',
                    snapshotRepo: 'springbootopenshift'
                )

                rtMavenResolver (
                    id: "maven_apache",
                    serverId: "artifactory",
                    releaseRepo: "springbootopenshift",
                    snapshotRepo: "springbootopenshift"
                )
            }
        }

        stage ('Build') {
            steps {
                rtMavenRun (
                    tool: 'maven_apache', // Tool name from Jenkins configuration
                    pom: 'pom.xml',
                    goals: 'clean install',
                   // deployerId: "MAVEN_DEPLOYER",
                   // resolverId: "MAVEN_RESOLVER"
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
