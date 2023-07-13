pipeline {
    agent any
    // agent {
    //     docker {
    //         image 'maven:3.9.0-eclipse-temurin-11' 
    //         args '-v /root/.m2:/root/.m2' 
    //     }
    // }
    // options {
    //     skipStagesAfterUnstable()
    // }
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
        stage('Artificial Delay') {
            steps {
                script {
                    sleep(30) // Adds a delay of 30 seconds
                }
            }
        }
        stage('Deliver') {
            steps {
                sh './jenkins/scripts/deliver.sh'
            }
        }
    }
}
