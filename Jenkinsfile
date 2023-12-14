pipeline {
  agent any

  stages {
    stage('Build Artifact - Maven') {
      steps {

        sh "echo Running Unit Tests on Petclinic Application"
        sh "docker run --rm -v $HOME/.m2:/root/.m2 -v `pwd`:/app -w /app maven:3.8-openjdk-11 mvn clean package -DskipTests=true"
        archive 'target/*.jar'
        
      }
    }
      stage('Unit Tests -JUnit and Jacoco') {
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