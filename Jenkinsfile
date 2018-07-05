@Library("infra-deployment/standardPipeline@integration") _

pipeline {
    agent {
        label 'packer'
    }
    environment {
      def terraform  = "docker run --rm -w /tf/sources/stacks/applications/alb-based/infra -v ${env.WORKSPACE}/:/tf hashicorp/terraform:light"
      def packer     = "docker run --rm -w /packer/sources/stacks/applications/alb-based/packer -v ${env.WORKSPACE}/:/packer"
    }
    stages {
      stage ('Start') {
        steps {
          script {
            sh "echo 'been here'"
          }
        }
      }

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
