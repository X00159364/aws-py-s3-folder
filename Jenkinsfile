pipeline {
    agent any

    environment {
        BUILD_URL = "${BUILD_URL}"
    }

    script{
        try {
            stages {
            
                stage ("Pulumi up") {
                    steps {
                        // The value "node 8.9.4" is the configuration name in our Global Tool Configuration setup for node.
                        // You should use the name that you used when you added the installation on that page.
                        nodejs(nodeJSInstallationName: "Node") {
                            withEnv(["PATH+PULUMI=C:/ProgramData/chocolatey/lib/pulumi/tools/Pulumi/bin"]) {
                                bat "pulumi stack select ${PULUMI_STACK}"
                                bat "pulumi up --yes"
                            }
                        }
                    }
                }
                
                stage ("Pulumi Destroy") {
                    steps {
                        // The value "node 8.9.4" is the configuration name in our Global Tool Configuration setup for node.
                        // You should use the name that you used when you added the installation on that page.
                        nodejs(nodeJSInstallationName: "Node") {
                            withEnv(["PATH+PULUMI=C:/ProgramData/chocolatey/lib/pulumi/tools/Pulumi/bin"]) {
                                sleep(60)
                                bat "pulumi stack select ${PULUMI_STACK}"
                                bat "pulumi destroy --yes"
                            }
                        }
                    }
                }
            }

            currentBuild.result = 'SUCCESS' // sets the ordinal as 0 and boolean to true        
        } catch (err) {
            currentBuild.result = 'FAILURE' // sets the ordinal as 4 and boolean to false
            throw err
        } finally {
            influxDbPublisher(selectedTarget: 'JenkinsDB')
        }  
        // post {
        //     always {
        //         influxDbPublisher(selectedTarget: 'JenkinsDB')
        //     }
        // }    
    }

}

def assignURL(build_url) {
    def buildURL = [:]
    buildURL['url'] = build_url
    return buildURL
}
