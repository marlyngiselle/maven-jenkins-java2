pipeline {
    agent any

    tools { maven "supermaven" }

    stages {

        stage('Code') {
            steps {
                git 'https://github.com/marlyngiselle/maven-jenkins-java2.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean install'
                // sh 'docker stop contenedor'
                // sh 'docker rm contenedor'
                sh 'docker build -t mgiselle/${JOB_NAME}:v${BUILD_NUMBER} .'
            }
        }

        stage('Test') {
            steps {
                echo 'Ingresa en la pagina y prueba tu mismo'
            }
        }

        stage('Release') {
            steps {
                sh 'docker tag mgiselle/${JOB_NAME}:v${BUILD_NUMBER} mgiselle/${JOB_NAME}:latest'
                sh 'docker login -u="mgiselle" -p="Tasia.2411"'
                sh 'docker push mgiselle/${JOB_NAME}:v${BUILD_NUMBER}'
                sh 'docker push mgiselle/${JOB_NAME}:latest'
                sh 'docker rmi mgiselle/${JOB_NAME}:v${BUILD_NUMBER}'
                sh 'docker rmi mgiselle/${JOB_NAME}:latest'
            }
        }

        stage('Deploy') {
            steps {
                sh 'docker run -d -p 80:8080 --name contenedor mgiselle/${JOB_NAME}:latest'
            }
        }

    }
}