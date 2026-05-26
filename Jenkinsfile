pipeline {

    agent {
        label 'agent2'
    }

    environment {
        DockerUsername = credentials('Docker-username')
        DockerPassword = credentials('Docker-password')
    }
    tools{
      jdk 'jdk-11'
      maven 'maven-354'
    }

    stages {

        stage('Build Java app') {
            steps {
                sh "mvn package -DskipTests"
            }
        }

        stage('Test Java app') {
            steps {
                sh 'mvn test'
            }
        }

        stage('Archive Java app') {
            steps {
                archiveArtifacts artifacts: '**/*.jar', followSymlinks: false
            }
        }

        stage('Build Docker image') {
            steps {
                sh 'docker build -t java-app-img1:v1 .'
            }
        }

        // stage('Login Docker') {
        //     steps {
        //         sh '''
        //             docker login -u $DockerUsername -p $DockerUsername
        //         '''
        //     }
        // }

        // stage('Push Docker image') {
        //     steps {
        //         sh 'docker push java-app-img1:v1'
        //     }
        // }

    }
}