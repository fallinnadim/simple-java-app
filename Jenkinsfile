pipeline {
    triggers {
        pollSCM('TZ=Asia/Jakarta\nH/2 * * * *')
           }
    agent {
        docker {
            image 'maven:3.9.5-eclipse-temurin-17-alpine'
            args '-v /root/.m2:/root/.m2'
        }
    }
    stages {
        stage('Build') {
            steps {
                sh 'maven -B -DskipTests clean package'
            }
        }
    }
}