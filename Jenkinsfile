pipeline {
  agent any

  stages {
    stage('Build Artifact - Maven') {
      steps {
        sh "git clone https://github.com/abbabe/devsecops-k8s.git"
        sh "cd devsecops-k8s"
        sh "mvn clean package -DskipTests=true"
        archive 'target/*.jar'
      }
    }

    stage('Unit Tests - JUnit and Jacoco') {
      steps {
        sh "mvn test"
      }
      post {
        always {
          junit 'target/surefire-reports/*.xml'
          jacoco execPattern: 'target/jacoco.exec'
        }
      }
    }
  }
}