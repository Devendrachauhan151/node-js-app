pipeline {
  agent any

  stages {
    stage('Build') {
      steps {
        // Checkout the repository
        git 'https://github.com/Devendrachauhan151/the-example-app.nodejs.git'

        // Build the Docker image
        script {
          docker.build("Node-app234:latest")
        }
      }
    }

    stage('Push') {
      steps {
        // Login to Docker Hub
        withCredentials([usernamePassword(credentialsId: 'your-credentials-id', passwordVariable: 'DOCKERHUB_PASSWORD', usernameVariable: 'DOCKERHUB_USERNAME')]) {
          sh 'docker login -u $devendradocker3212 -p $dckr_pat_yRXAXiqyt3lxq9GhuLVjbJ7vwFk'
        }

        // Push the Docker image to Docker Hub
        script {
          docker.withRegistry('https://registry.hub.docker.com', 'docker-hub-credentials') {
            dockerImage.push()
          }
        }
      }
    }

    stage('Deploy') {
      steps {
        // Deploy the Docker container to your server
        sh 'docker-compose up -d'
      }
    }
  }

  post {
    success {
      echo 'Deployment successful!'
    }

    failure {
      echo 'Deployment failed!'
    }
  }
}
