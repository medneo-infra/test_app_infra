@Library("infra-deployment@feature/refactoring") _

import static com.deployment.ReleaseIDGenerator.*

pipeline {
  agent {
        node {
            label 'lol'
        }
    }
    stages {
      stage ('compile') {
        steps {
          operator = generate this
          operator.operate this
        }
      }
    }
  }