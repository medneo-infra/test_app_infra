@Library("infra-deployment@feature/nodes") _

import com.deployment.GlobalVars
def Class GlobalVars_local = GlobalVars

def deployConfig = [
  appName : "scheduling",
  appCommit : "21e32d7460ab84c8e76b8de9d21fd1d05a7c48ef",
  //appCommit : "latest",
  terraformProject : "customer-service",
  featureBranch: "feature/nodes",

  stagingBranch : "development",
  stagingAutoscalingGroupMin : "1",
  stagingAutoscalingGroupMax : "2",
  stagingInstanceType : "t2.micro",

  releasePrefix : "release",
  releaseAutoscalingGroupMin : "1",
  releaseAutoscalingGroupMax : "2",
  releaseInstanceType : "t2.micro",

  productionBranch : "master",
  prodAutoscalingGroupMin : "1",
  prodAutoscalingGroupMax : "2",
  prodInstanceType : "t2.micro"
]

pipeline {
  agent {
        node {
            label 'lol'
        }
    }
    stages {
      stage ('compile') {
        steps {
          echo "done compiling"
        }
      }
      stage ('Deployment') {
        agent { label 'packer' }
        when {
            beforeAgent true
            allOf {
              expression { return prepDeployment(deployConfig, GlobalVars_local) }
              anyOf {
                expression { GlobalVars_local.FEATURE_BRANCH != null }
                expression { return GlobalVars_local.STAGING_DECISION }
                expression { return GlobalVars_local.RELEASE_DECISION }
                expression { return GlobalVars_local.PRODUCTION_DECISION }
              }
            }
        }
        steps {
            script {
              doCheckout()
              if (GlobalVars_local.BUILD_DECISION) {
                amiBuild(deployConfig, GlobalVars_local)
              }
              amiDeployment(deployConfig, GlobalVars_local)
            }
        }
      }
    }
}
