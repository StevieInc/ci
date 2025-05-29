node {
  label 'docker'

  stage('Checkout') {
    checkout scm
  }

  stage('Build & Push') {
    docker.withRegistry('https://index.docker.io/v1', '1') {
      def image = docker.build("hack3rru/demo-tms:groovy")
      image.push()
    }
  }
}
