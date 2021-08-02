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

    stage('install dependencies') {
      steps {
        sh 'npm install'
      }
    }

    stage('run the app') {
      steps {
        sh 'npm start &'
      }
    }

    stage('test the app') {
      steps {
        sh 'sleep 5 && curl localhost:8080'
      }
    }

    stage('kill the app') {
      steps {
        sh ' pkill -f node'
      }
    }

    stage('Package') {
      steps {
        sh 'zip -r package.zip .'
        archiveArtifacts(artifacts: 'package.zip', onlyIfSuccessful: true)
        cleanWs(cleanWhenSuccess: true)
      }
    }

    stage('Notify_Slack') {
      steps {
        slackSend(channel: 'dd_devops', color: '#3EA652', message: "Success: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]' (${env.BUILD_URL})")


      }
    }

  }
}
