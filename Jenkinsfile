@Library("infra-deployment/standardPipeline@integration") _

pipeline {
    agent {
        label 'packer'
    }
    stages {
      stage ('Start') {
        steps {
          script {
            sh "echo 'been here'"
          }
        }
      }
      stage ('Shared stages') {
        standardPipeline {
          appName = "scheduling"
          appCommit = "latest"

          stagingBranch = "development"
          stagingAutoscalingGroupMin = "1"
          stagingAutoscalingGroupMax = "2"
          stagingInstanceType = "t2.micro"

          releasePrefix = "release"
          releaseAutoscalingGroupMin = "1"
          releaseAutoscalingGroupMax = "2"
          releaseInstanceType = "t2.micro"

          productionBranch = "master"
          prodAutoscalingGroupMin = "1"
          prodAutoscalingGroupMax = "2"
          prodInstanceType = "t2.micro"
        }
      }
    }
  }
