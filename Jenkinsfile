    @Library("infra-deployment/standardPipeline") _
    standardPipeline {
        appName = "scheduling"
        appCommit = "60ba047"
        productionBranch = "master"
        stagingBranch = "development"
        stagingAutoscalingGroupMin = "1"
        stagingAutoscalingGroupMax = "2"
        stagingInstanceType = "t2.micro"
        prodAutoscalingGroupMin = "1"
        prodAutoscalingGroupMax = "2"
        prodInstanceType = "t2.micro"
    }
