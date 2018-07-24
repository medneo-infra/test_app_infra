@Library("infra-deployment/standardPipeline@feature/nodes") _
import com.deployment.GlobalVars
def deployConfig = [
  appName : "scheduling",
  appCommit : "5802d8fdb589b149575514121421ede360489739",
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
            echo "On _lol_ node"
            //standardPipeline.prepDeployment deployConfig
            standardPipeline.sayHello("Schtring")
          }
        }
      }

      stage ('Deploy') {
        agent {
          label 'packer'
        }
        steps {
            script {
              echo "On _packer_ node"
              standardPipeline.doDeployment deployConfig
            }
        }
      }
  }
}
