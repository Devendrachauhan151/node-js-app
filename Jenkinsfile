pipeline {
  agent any

  stages {
    stage('Build') {
      steps {
        withCredentials([usernamePassword(credentialsId: 'Devendrachauhan151', passwordVariable: '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', usernameVariable: 'Devendrachauhan151')]) {
          // Checkout the Git repository with the provided credentials
  
        // Build the Docker image
        script {
          docker.build("Node-app1234:latest")
        }
      }
    }

    stage('Push') {
      steps {
        // Login to Docker Hub
        withCredentials([usernamePassword(credentialsId: 'devendradocker3212', passwordVariable: 'dckr_pat_4wiVzGjMYnw0rsql0BA9P6XlHSk', usernameVariable: 'devendradocker3212')]) {
          sh 'docker login -u $DOCKERHUB_USERNAME -p $DOCKERHUB_PASSWORD'
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
}
