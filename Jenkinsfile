@Library("infra-deployment@feature/refactoring") _

import com.deployment.GlobalVars
import com.deployment.PipelineFactory
def Class GlobalVars_local = GlobalVars
PipelineFactory PipelineFactory_local = PipelineFactory

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
  cloudEnvironmentVer : "*/development",
  cloudEnvironmentGit : "https://github.com/medneo/arc-az-infrastructure",
  cloudEnvironmentSrc : "/stacks/applications/alb_based"
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
              /* def cloud_env = factory.setCloudEnvironment(GlobalVars_local) */
              PipelineFactory_local.setCloudEnvironment(GlobalVars_local)
              /* if (GlobalVars_local.BUILD_DECISION) {
                cloud_env.amiBuild(deployConfig, GlobalVars_local)
              }
              cloud_env.amiDeploy(deployConfig, GlobalVars_local) */
            }
          }
        }
      }
    }
