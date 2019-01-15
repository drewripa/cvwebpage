pipeline {
  agent {
    label 'linux'
  }
  stages {
    stage ('Checkout') {
      checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[url: 'https://github.com/drewripa/cvwebpage.git']]])
    }
    stage ('Raise Container') {
      script {
        def containerID = sh (
          script: 'docker ps --filter name=nginx -q',
          returnStatus: true
          )
        if (containerID == '') {
          sh 'docker run --name nginx --restart always -d -p 80:80 -v \$(pwd):/usd/share/nginx/html nginx:latest'
        } else {

        }
      }
    }
  }
}
