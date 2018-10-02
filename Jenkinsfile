@Library("infra-deployment@development") _

import com.deployment.GlobalVars
def Class GlobalVars_local = GlobalVars

def deployConfig = [
  appName : "testapp",
  appCommit : "latest",
  terraformProject : "internal-mgmt",
  //featureBranch: "feature/azure",
  deploymentType: "docker",

  stagingBranch : "development",
  stagingAutoscalingGroupMin : "1",
  stagingAutoscalingGroupMax : "1",
  stagingInstanceType : "t2.micro",

  releasePrefix : "release",
  releaseAutoscalingGroupMin : "1",
  releaseAutoscalingGroupMax : "1",
  releaseInstanceType : "t2.micro",

  productionBranch : "master",
  prodAutoscalingGroupMin : "1",
  prodAutoscalingGroupMax : "1",
  prodInstanceType : "t2.micro",

  healthEndpoint : "/"
]

pipeline {
  agent {
        node {
            label '20GB'
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
