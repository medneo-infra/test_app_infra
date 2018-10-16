@Library("infra-deployment@feature/refactoring") _

import static com.deployment.*

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
          doThis
          sh "ls"
        }
      }
    }
  }