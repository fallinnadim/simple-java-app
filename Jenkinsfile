// node {
//     properties([pipelineTriggers([pollSCM('TZ=Asia/Jakarta\nH/2 * * * *')])])
//     docker.image('maven:3.9.5-eclipse-temurin-17-alpine').inside('-v /root/.m2:/root/.m2') {
//         stage('Build') {
//             sh 'mvn -B -DskipTests clean package'
//         }
//         stage('Test') {
//             try {
//                 sh 'mvn test'
//             } catch (e){
//                 echo 'test went wrong'
//                 throw (e)
//             } finally {
//                 junit 'target/surefire-reports/*.xml'
//             }
//         }
//     }
// }

pipeline {
    agent {
        docker {
            image 'maven:3.9.5-eclipse-temurin-17-alpine'
            args '-v /root/.m2:/root/.m2'
        }
    }
    triggers {
        pollSCM 'TZ=Asia/Jakarta\nH/2 * * * *'
    }
    stages {
        stage('Build') {
            steps {
                sh 'mvn -B -DskipTests clean package'
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test'
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }
    }
}