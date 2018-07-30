@Library("infra-deployment@feature/nodes") _

import com.deployment.GlobalVars
def Class GlobalVars_local = GlobalVars

def deployConfig = [
  appName : "scheduling",
  //appCommit : "5802d8fdb589b149575514121421ede360489739",
  appCommit : "latest",
  terraformProject : "customer-service",
  //featureBranch: "feature/nodes",

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
                expression { return GlobalVars_local.STAGING_DECISION.toBoolean() }
                expression { return GlobalVars_local.RELEASE_DECISION.toBoolean() }
                expression { return GlobalVars_local.PRODUCTION_DECISION.toBoolean() }
              }
            }
        }
        steps {
            script {
              echo "On _packer_ node"
              doCheckout()
              if (GlobalVars_local.BUILD_DECISION.toBoolean()) {
                amiBuild(deployConfig, GlobalVars_local)
              }
              amiDeployment(deployConfig, GlobalVars_local)
            }
        }
      }
    }
}
