pipeline {
  agent {
    node {
      label 'docker'
    }

  }
  stages {
    stage('checkout') {
      steps {
        git(url: 'https://github.com/anasshwi/node-docker-good-defaults', branch: 'main', changelog: true, poll: true)
      }
    }

    stage('build') {
      steps {
        sh 'docker build -t nodeA:$BUILD_ID .'
      }
    }

    stage('run & test') {
      steps {
        sh 'docker run --name nodeA -d -p 9229:9230 nodeA:$BUILD_ID'
        sleep 3
        sh 'curl localhost:8080'
        sh 'docker stop nodeA && docker rm nodeA'
      }
    }

    stage('push') {
      steps {
        sh 'docker tag nodeA:$BUILD_ID anasshwi/good_node_app:$BUILD_ID'
        sh 'docker login -u anasshwi -p Anas123456'
        sh 'docker push anasshwi/good_node_app:$BUILD_ID'
      }
    }

  }
}