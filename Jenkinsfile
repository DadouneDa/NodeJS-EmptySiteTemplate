pipeline {
  agent {
    node {
      label 'centos7'
    }

  }
  stages {
    stage('Checkout_code') {
      steps {
        git(url: 'https://github.com/DadouneDa/NodeJS-EmptySiteTemplate.git', branch: 'master', changelog: true, poll: true, credentialsId: 'dd_github')
      }
    }

  }
}