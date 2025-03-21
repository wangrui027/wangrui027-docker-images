pipeline {
  agent any
  stages {
    stage('检出代码') {
      steps {
        checkout([
          $class: 'GitSCM',
          branches: [[name: GIT_BUILD_REF]],
          userRemoteConfigs: [[
            url: GIT_REPO_URL,
            credentialsId: CREDENTIALS_ID
          ]]
        ])
      }
    }
    stage('docker login') {
      steps {
        sh "echo \"${env.DOCKER_PASSWORD}\" | docker login -u wangrui027 --password-stdin"
      }
    }
    stage('构建推送 almalinux') {
      steps {
        sh 'almalinux/build.sh'
      }
    }
    stage('构建推送 openjdk') {
      steps {
        sh 'openjdk/build.sh'
      }
    }
    stage('构建推送 tomcat') {
      steps {
        sh 'tomcat/build.sh'
      }
    }
  }
  post {
    failure {
      echo 'Build and deployment failed!'

    }

    success {
      echo 'Build and deployment succeeded!'

    }

  }
}