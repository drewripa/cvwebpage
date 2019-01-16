pipeline {
  agent {
    label 'linux'
  }
  stages {
    stage ('Checkout') {
      steps {
        script {
          withCredentials([usernamePassword(credentialsId: 'telegram_chatid_token', passwordVariable: 'TGTOKEN', usernameVariable: 'TGCHAT')]) {
              MESSAGE = ":rotating_light: Build ${BUILD_NUMBER} started."
              sh "curl -s -X POST https://api.telegram.org/bot${TGTOKEN}/sendMessage -d chat_id=${TGCHAT} -d text=$\'${MESSAGE}\'"
            }
          }
        checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[url: 'https://github.com/drewripa/cvwebpage.git']]])
      }
    }
    stage ('Raise Container') {
      steps {
        script {
          containerID = sh (
            script: 'docker ps --filter name=httpd -q',
            returnStdout: true
            )
          if (containerID == '') {
            sh 'docker run --name httpd --restart always -d -p 80:80 -v \$(pwd):/usr/local/apache2/htdocs/ httpd:latest'
          } else {
            echo "Container ${containerID} exists"
          }
        }
      }
    }
  }
  post {
    success {
        script {
          withCredentials([usernamePassword(credentialsId: 'telegram_chatid_token', passwordVariable: 'TGTOKEN', usernameVariable: 'TGCHAT')]) {
              MESSAGE = ":sunny: Build ${BUILD_NUMBER} finished successfully."
              sh "curl -s -X POST https://api.telegram.org/bot\${TGTOKEN}/sendMessage -d chat_id=\${TGCHAT} -d text=$\'\${MESSAGE}\'"
          }
        }
    }
    failure {
        script {
          withCredentials([usernamePassword(credentialsId: 'telegram_chatid_token', passwordVariable: 'TGTOKEN', usernameVariable: 'TGCHAT')]) {
              MESSAGE = ":cloud_lightning: Build ${BUILD_NUMBER} finished with errors."
              sh 'curl -s -X POST https://api.telegram.org/bot"${TGTOKEN}"/sendMessage -d chat_id="${TGCHAT}" -d text=$\'${MESSAGE}\''
          }
        }
    }
  }
}
