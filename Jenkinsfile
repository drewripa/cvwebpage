pipeline {
  agent {
    label 'linux'
  }
  stages {
    stage ('Checkout') {
      steps {

        checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[url: 'https://github.com/drewripa/cvwebpage.git']]])
      }
    }
    stage ('Raise Container') {
      steps {
        script {
          containerID = sh (
            script: 'docker ps --filter name=nginx -q',
            returnStdout: true
            )
          if (containerID == '') {
            sh 'docker run --name nginx --restart always -d -p 80:80 -v \$(pwd):/usr/share/nginx/html nginx:latest'
          } else {
            echo "Container ${containerID} exists"
          }
        }
      }
    }
  }
}
