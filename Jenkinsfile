@Library("infra-deployment/standardPipeline@ARC-299") _
standardPipeline {
    appName = "scheduling"
    appCommit = "60ba047"

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
