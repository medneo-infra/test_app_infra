@Library("infra-deployment@feature/refactoring") _

import com.deployment.*
def Class GlobalVars_local = GlobalVars

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

node {
  stage('Test') {
    doThis
    sh "echo 'I was here'"
    sh "echo '${doThis}'"
  }
}
