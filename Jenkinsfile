pipeline {
    agent any
    
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
                        bat "pulumi stack select ${PULUMI_STACK}"
                        //bat "pulumi destroy --yes"
                    }
                }
            }
        }
    }
}