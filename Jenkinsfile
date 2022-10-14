pipeline {
    agent { 
	node { label 'MVN3' }
        }
	    stages {
        stage('vcs') {
            steps {
             git url: 'https://github.com/nagarjunaduggireddy/openmrs-core.git', 
             branch: 'master'
            }
			}
	stage ('Artifactory configuration') {
            steps {
                
           rtMavenDeployer (
           id: "MAVEN_DEPLOYER",
           serverId: "openmrs-jfrog",
           releaseRepo: 'default-libs-release-local',
           snapshotRepo: 'default-libs-snapshot-local'
                )

            }
        }
stage ('Exec Maven') {
            steps {
                rtMavenRun (
                    tool: 'MVN_DEFAULT', 
                    pom: 'pom.xml',
                    goals: 'clean install',
                    deployerId: "MAVEN_DEPLOYER"
                )
            }
        }
			stage ('Publish build info') {
            steps {
                rtPublishBuildInfo (
                    serverId: "JFROG_OCT22"
                )
            }
        }
    }
}
