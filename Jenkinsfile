pipeline {
    agent any
    environment {
	MAVEN_USER_HOME="/home/jenkins/.m2" 	 
    }
    stages {
        stage('Build') {
            steps {
                sh './mvnw -B clean package spring-boot:repackage'
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
                nexusPublisher nexusInstanceId: 'Nexus-Oss', nexusRepositoryId: 'maven-releases', packages: [[$class: 'MavenPackage', mavenAssetList: [], mavenCoordinate: [artifactId: 'hello', groupId: 'com.example', packaging: 'jar', version: '0.0.1']]]
            }
        }
    }
}
