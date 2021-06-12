pipeline {
    agent any
    stages {
        stage ('Clone') {
            steps {
                git branch: 'master', url: "https://github.com/vipinpatel84/springbootopenshift.git"
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
                    releaseRepo: "http://localhost:8081/artifactory/springbootopenshift",
                    snapshotRepo: "http://localhost:8081/artifactory/springbootopenshift"
                )

                rtMavenResolver (
                    id: "maven_apache",
                    serverId: "artifactory",
                    releaseRepo: "http://localhost:8081/artifactory/springbootopenshift",
                    snapshotRepo: "http://localhost:8081/artifactory/springbootopenshift"
                )
            }
        }

        stage ('Exec Maven') {
            steps {
                rtMavenRun (
                    tool: 'maven_apache', // Tool name from Jenkins configuration
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
                    serverId: "ARTIFACTORY_SERVER"
                )
            }
        }
    }
}
