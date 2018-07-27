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
          }
        }
      }

      stage ('Deploy') {
        agent {
          label 'packer'
        }
        steps {
            script {
              @Library("infra-deployment/standardPipeline@feature/alb_healthcheck") _
              def deployConfig = [
                appName : "scheduling",
                appCommit : "5802d8fdb589b149575514121421ede360489739",
                //appCommit : "latest",
                terraformProject : "customer-service",
                featureBranch: "feature/alb_healthcheck",

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
                prodInstanceType : "t2.micro",

                healhEndpoint : "/"
              ]
              standardPipeline(deployConfig)
            }
        }
      }
  }
}
