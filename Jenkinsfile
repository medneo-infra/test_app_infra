@Library("infra-deployment@feature/refactoring") _

import static com.deployment.PipelineFactory.*
import static com.deployment.Azure.*
import static com.deployment.Aws.*
import static com.deployment.Vault.*
import static com.deployment.Checkouter.*
import static com.deployment.Builder.*
import static com.deployment.Deployer.*
import com.deployment.GlobalVars
def Class GlobalVars_local = GlobalVars

def deployConfig = [
  appName : "testapp",
  appCommit : "latest",
  terraformProject : "internal-mgmt",
  deploymentType : "docker",
  configBranch : "development",
  featureBranch : "feature/azure",
  cloudEnvironment : "azure",
  cloudEnvironmentVer : "*/development",

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
            prepDeployment
            cloud = setCloudEnvironment this, GlobalVars_local
            sh "ls"
            sh "aws s3 ls"
            cloud.amiBuild this, deployConfig, GlobalVars_local
          }
        }
      }
    }
  }