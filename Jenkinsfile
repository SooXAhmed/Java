pipeline {

    agent {
        label 'agent2'
    }

    environment {
        DockerUsername = credentials('Docker-username')
        DockerPassword = credentials('Docker-password')
        JAVA_HOME = '/usr/lib/jvm/java-21-openjdk-21.0.10.0.7-2.el9.x86_64'
        PATH = "${JAVA_HOME}/bin:${env.PATH}"
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

        stage('Login Docker') {
            steps {
                sh '''
                    docker login -u $DockerUsername_USR -p $DockerUsername_PSW
                '''
            }
        }

        // stage('Push Docker image') {
        //     steps {
        //         sh 'docker push java-app-img1:v1'
        //     }
        // }

    }
}