pipeline {
    agent any
    
    stages {
        stage('Build') {
            steps {
                sh './mvnw -B clean package spring-boot:repackage'
		nexusPolicyEvaluation iqApplication: selectedApplication('sandbox-application'), iqScanPatterns: [[scanPattern: 'target/*jar']], iqStage: 'build'
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
                nexusPublisher nexusInstanceId: 'Nexus-Oss', nexusRepositoryId: 'maven-releases', packages: [[$class: 'MavenPackage', mavenAssetList: [[classifier: '', extension: '', filePath: '/var/lib/jenkins/workspace/Test-Branch/target/hello-0.0.1-SNAPSHOT.jar']], mavenCoordinate: [artifactId: 'hello', groupId: 'com.example', packaging: 'jar', version: '0.0.1']]]
            }
        }
    }
}
