pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                sh 'cd hello && ./mvnw -B clean package spring-boot:repackage'
            }
        }
        stage('Test') {
            steps {
                sh './mvnw -B test && ./mvnw jacoco:report'
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }
        stage('Deploy') {
            steps {
                sh 'echo deployment unimplemented'
            }
        }
    }
}
