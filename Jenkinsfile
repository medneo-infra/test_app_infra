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
            //echo "${GlobalVars.GIT_COMMIT}"
          }
        }
      }

      stage ('Deploy') {
        agent {
          label 'packer'
        }
        steps {
            script {
              @Library("infra-deployment/standardPipeline@master") _
              def deployConfig = [
                appName : "scheduling",
                appCommit : "5802d8fdb589b149575514121421ede360489739",
                terraformProject : "customer-service",
                //featureBranch: "feature/nodes",

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
              standardPipeline(deployConfig)
              //echo "Been here too"
            }
        }
      }
  }
}
