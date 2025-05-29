pipeline {
  agent { label 'docker' }

  environment {
    REGISTRY_URL = 'https://registry.hub.docker.com'
    IMAGE_NAME   = "${REGISTRY_URL}/hack3rru/demo-tms"
    CREDS_ID     = '1'
  }

  stages {
    stage('Checkout') {
      steps {
        checkout scm
      }
    }

    stage('Build') {
      steps {
        script {
          // Логин в реестр
          docker.withRegistry(REGISTRY_URL, CREDS_ID) {
            // Сборка образа
            docker.build("${IMAGE_NAME}:groovy")
          }
        }
      }
    }

    stage('Push') {
      steps {
        script {
          docker.withRegistry(REGISTRY_URL, CREDS_ID) {
            // Пушим оба тега: по номеру билда и latest
            docker.image("${IMAGE_NAME}:${env.BUILD_NUMBER}").push()
          }
        }
      }
    }
  }

  post {
    always {
      echo "Pipeline finished. Проверить образы в ${IMAGE_NAME}"
    }
  }
}
