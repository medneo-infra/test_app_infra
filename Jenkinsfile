    @Library("infra-deployment/standardPipeline") _
    standardPipeline {
        appName = "scheduling"
        appCommit = "b91ccf8"
        productionBranch = "master"
        stagingBranch = "development"
        stagingAutoscalingGroupMin = "1"
        stagingAutoscalingGroupMax = "2"
        stagingInstanceType = "t2.micro"
        prodAutoscalingGroupMin = "2"
        prodAutoscalingGroupMax = "4"
        prodInstanceType = "t2.medium"
    }
