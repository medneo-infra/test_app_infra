pipeline {
  agent {
        node {
            label 'lol'
        }
    }
    stages {
      stage ('Start') {
        steps {
          script {
            sh "echo 'been here'"
            echo "${GlobalVars.GIT_COMMIT}"
          }
        }
      }

      stage ('Deploy') {
        agent {
          label 'packer'
        }
        steps {
            script {
              // standardPipeline(deployConfig)
              echo "Been here too"
            }
        }
      }
  }
}

@Library("infra-deployment/standardPipeline@feature/nodes") _
def deployConfig = [
  appName : "scheduling",
  appCommit : "latest",
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