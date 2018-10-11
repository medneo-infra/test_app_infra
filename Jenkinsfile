@Library("infra-deployment@feature/refactoring") _

import com.deployment.GlobalVars
import com.deployment.CloudHelpers
def Class GlobalVars_local = GlobalVars
def Class Cloud = PipelineFactory

def deployConfig = [
  appName : "testapp",
  appCommit : "latest",
  terraformProject : "customer-service",
  featureBranch: "feature/azure",
  deploymentType: "docker",

  stagingBranch : "development",
  stagingAutoscalingGroupMin : "1",
  stagingAutoscalingGroupMax : "1",
  stagingInstanceType : "Standard_A0",

  releasePrefix : "release",
  releaseAutoscalingGroupMin : "1",
  releaseAutoscalingGroupMax : "1",
  releaseInstanceType : "Standard_A0",

  productionBranch : "master",
  prodAutoscalingGroupMin : "1",
  prodAutoscalingGroupMax : "1",
  prodInstanceType : "Standard_A0",

  healthEndpoint : "/",

  cloudEnvironment : "azure",
  cloudEnvironmentVer : "*/development"
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
              a = Cloud.setCloudEnvironment(GlobalVars_local)
              a.doCheckout()
              if (GlobalVars_local.BUILD_DECISION) {
                a.amiBuild(deployConfig, GlobalVars_local)
              }
              a.amiDeploy(deployConfig, GlobalVars_local)
            }
          }
        }
      }
    }
