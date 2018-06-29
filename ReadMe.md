# Example project for AWS infrastructure and Jenkins integration

Utilising the Jenkins shared library and the [AWS Customer Services Infrastructure](https://github.com/medneo/infrastructure_customerservices)

If you want that too, your project needs

* to be registered (please reach out to @dassbj01)
* have 3 basic files included at top level
  * Jenkinsfile
  * docker-compose.yml
  * .env

Your environment will be updated automatically for a *production* and *development* branch, as defined in the Jenkinsfile. The FQDN will be printed at the end of the Jenkins build.

Example usage in `test_app_infra`
- [GitHub](https://github.com/medneo/test_app_infra)
- [Jenkins](https://jenkins.medneo.com/job/medneo-org-folder/job/test_app_infra/)

## Jenkinsfile
The Jenkinsfile calls a shared library which updates the AWS infrastructure with your recent code.
```
@Library("infra-deployment/standardPipeline") _
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

```

### Variables
Name                        | Purpose | example value
----                        | ------- | -------------
appName                     | this is the registered name of the application and part of the FQDN | scheduling
appCommit                   | if you want to pin the deployed app to a certain commit (aka version) | either 'latest' or a GitCommit ID (short or long)
productionBranch            | what is the production branch | master
stagingBranch               | what is the staging branch | development
stagingAutoscalingGroupMin  | minimum number of machines running in staging | 1
stagingAutoscalingGroupMax  | maximum number of machines running in staging | 2
stagingInstanceType         | instance type (size) in staging; see https://aws.amazon.com/ec2/instance-types/ | t2.micro
prodAutoscalingGroupMin     | minimum number of machines running in production | 1
prodAutoscalingGroupMax     | maximum number of machines running in production | 2
prodInstanceType            | instance type (size) in prod; see https://aws.amazon.com/ec2/instance-types/ | t2.micro
releasePrefix               | the prefix to separate the actual name from | release
releaseAutoscalingGroupMin  | minimum number of machines running in production | 1
releaseAutoscalingGroupMax  | maximum number of machines running in production | 2
releaseInstanceType         | instance type (size) in prod; see https://aws.amazon.com/ec2/instance-types/ | t2.micro

## docker-compose.yml
Please provide a valid `docker-compose.yml` file which will be run via docker-compose

```
web:
  image: "nginx:${TAG}"
  ports:
   - "80:80"
  command: /bin/bash -c "exec nginx -g 'daemon off;'"
```

## .env
Please provide a valid `.env` file which is placed right next to the above `docker-compose.yml` file.
```
TAG=latest
```
