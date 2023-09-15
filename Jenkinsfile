pipeline {
    agent any

    stages {
        stage('cleanup') {
            steps {
                cleanWs()
            }
        }
        stage('Build') {
            steps {
                sh 'echo Hello World!'
            }
        }
        stage('create file') {
            steps {
               sh "uuidgen | xargs touch"
            }
        }
    }
}
