pipeline {
    agent any
  tools {
      jdk "jdk-17"
        maven 'maven-3'
    }
    stages {
        stage('Build') {
            steps {
                  git(url: 'http://github.com/spring-projects/spring-petclinic.git', branch: 'main')
                  sh 'mvn clean verify'
            }
        }
        stage('Build & Test') {
                steps {
                    sh 'mvn clean test'
                }
                post {
                    always {
                        junit '**/target/surefire-reports/*.xml'
                    }
                    success {
                        slackSend (color: 'good', message: "SUCCESS: Job '${env.BUILD_TAG}' <${env.BUILD_URL}|link> completed successfully.", channel: "#jenkins-konrad-zochowski")
                    }
                    failure {
                        slackSend (color: 'danger', message: "FAILURE: Job '${env.BUILD_TAG}' <${env.BUILD_URL}|link> has failed.", channel: "#jenkins-konrad-zochowski")
                    }
                    unstable {
                        slackSend (color: 'warning', message: "UNSTABLE: Job '${env.BUILD_TAG}' <${env.BUILD_URL}|link> is unstable.", channel: "#jenkins-konrad-zochowski")
                    }
                }
            }
        
    }
}
