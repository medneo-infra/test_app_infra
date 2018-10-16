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
          echo "done compiling"
          generate this
          sh "ls"
        }
      }
    }
  }