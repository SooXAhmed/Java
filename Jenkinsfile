pipeline{
    agent {
    label 'agent2'
    }
    environment {
    DockerUsername = credentials("Docker-username")
    DockerPassword = credentials("Docker-password")
    }
    stages {
  stage('Build java app') {
    steps {
      sh "mvn package install -DskipTests"
    }
  }

  stage('Test Java app') {
    steps {
      sh "mvn test"
    }
  }
  stage('Archive java app'){
    steps{
    archiveArtifacts artifacts: '**/*.jar', followSymlinks: false
    }
  }
    stage('Build Docker image') {
    steps {
      sh "docker build -t java-app-img1:v1 ."
    }
    stage('Login Docker') {
    steps {
      sh "docker login -u ${DockerUsername} -p ${DockerPassword}"
    }
    // stage('push Docker image') {
    // steps {
    //   sh "docker push -t java-app-img1:v1 ."
    // }
  }
  }
  


//archiveArtifacts artifacts: '**/*.jar', followSymlinks: false
}

}