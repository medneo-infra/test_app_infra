@Library("infra-deployment@feature/nodes") _

// def globalVars_local = new com.deployment.GlobalVars() // Operation not permitted
import com.deployment.GlobalVars
def Class GlobalVars_local = GlobalVars

def deployConfig = [
  appName : "scheduling",
  //appCommit : "5802d8fdb589b149575514121421ede360489739",
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

pipeline {
  agent {
        node {
            label 'lol'
        }
    }
    stages {
      stage ('Prepare deployment') {
        steps {
          script {
            echo "On _lol_ node"
            prepDeployment(deployConfig, GlobalVars_local)
          }
        }
      }

      stage ('Build') {
        agent {
          label 'packer'
        }
        when {
          beforeAgent true
          expression { return GlobalVars_local.BUILD_DECISION.toBoolean() }
        }
        steps {
            script {
              echo "On _packer_ node"
              doCheckout()
              doBuild(deployConfig, GlobalVars_local)
            }
        }
        post {
          // cleanup as we checkout again
          always { dir('deploySrc') { deleteDir() } }
        }
      }
      //
      // stage ('Deploy') {
      //   agent {
      //     label 'packer'
      //   }
      //   when {
      //           beforeAgent true
      //           anyOf {
      //             expression { GlobalVars.FEATURE_BRANCH != null }
      //             expression { return GlobalVars.STAGING_DECISION.toBoolean() }
      //             expression { return GlobalVars.RELEASE_DECISION.toBoolean() }
      //             expression { return GlobalVars.PRODUCTION_DECISION.toBoolean() }
      //           }
      //   }
      //   steps {
      //       script {
      //         echo "On _packer_ node"
      //         doCheckout()
      //         doDeployment(deployConfig)
      //       }
      //   }
      // }
  }
}
