@Library("infra-deployment@feature/refactoring") _

import static com.deployment.PipelineFactory.*
/* import static com.deployment.Checkouter.* */
import com.deployment.GlobalVars
def Class GlobalVars_local = GlobalVars

def deployConfig = [
  funcName : "testapp",
  appCommit : "latest",
  terraformProject : "internal-mgmt",
  deploymentType : "docker",
  configBranch : "development",
  featureBranch : "feature/refactoring",
  cloudEnvironment : "azure",
  cloudEnvironmentVer : "refs/tags/v0.4",
  functionSource : "ReadMe.md",

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
            label 'lol'
        }
    }
    stages {
      stage ('compile') {
        steps {
          script {
            cloud = setCloudEnvironment this, GlobalVars_local
            cloud.doCheckout this, GlobalVars_local
            cloud.functionBuild this, deployConfig, GlobalVars_local
          }
        }
      }
    }
  }