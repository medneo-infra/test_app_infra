    @Library("infra-deployment/standardPipeline") _
    standardPipeline {
        appName = "scheduling"
        appCommit = "latest"
        stagingAutoscalingGroupMin = "1"
        stagingAutoscalingGroupMax = "2"
        stagingInstanceType = "t2.micro"
        prodAutoscalingGroupMin = "2"
        prodAutoscalingGroupMax = "4"
        prodInstanceType = "t2.medium"
    }
