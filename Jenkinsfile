pipeline {
    agent any
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
                    credentialsId: 'ARTIFACTORY_CRED',
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
                
                rtMavenRun (
                    tool: 'maven_apache', // Tool name from Jenkins configuration
                    pom: 'pom.xml',
                    goals: 'clean install deploy'
                //    deployerId: "maven_apache",
                //    resolverId: "maven_apache"
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
