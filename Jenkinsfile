@Library("infra-deployment@feature/refactoring") _

import static com.deployment.ReleaseIDGenerator.*
/* import com.deployment.GlobalVars
def Class GlobalVars_local = GlobalVars */
def APP_COMMIT = "latest"
def ARTIFACT_BUCKET = "18-000-arc-default-artifacts"

def deployConfig = [
  funcName : "testapp",
  appCommit : "latest",
  terraformProject : "internal-mgmt",
  deploymentType : "docker",
  configBranch : "development",
  featureBranch : "feature/refactoring",
  cloudEnvironment : "azure",
  cloudEnvironmentVer : "refs/tags/v0.4",
  functionSource : "ReadMe.md/",

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
            cloud = generate this
            cloud.setCloudEnvironment this deployConfig latest 18-000-arc-default-artifacts
          }
        }
      }
    }
  }