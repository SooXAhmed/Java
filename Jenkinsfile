@Library('First-Shared-Lib')_
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
            script{
                def allMavenFunctions=new org.package1.mavenClass()
                allMavenFunctions.build("package install -DskipTests")
            }

        }

        stage('Test Java app') {
            steps {
                script{
                    def allMavenFunctions=new org.package1.mavenClass()
                    allMavenFunctions.test()
                }
            }
        }

        stage('Archive Java app') {
            steps {
                archiveArtifacts artifacts: '**/*.jar', followSymlinks: false
            }
        }

        stage('Build Docker image') {
            steps {
                // script{
                //     allDockerFunctions=new edu.package1.DockerClass()
                // }
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