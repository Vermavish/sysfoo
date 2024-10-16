pipeline {
  agent {
  docker { image 'maven:3.9.6-eclipse-temurin-17' }
  }
  tools{
  maven 'Maven 3.6.3'
        }
  stages{
      stage("Build"){
          steps{
              echo 'Build: step 1'
              sh 'mvn compile'
          }
      }
      stage("Test"){
          steps{
              echo 'Test: step 2'
              sh 'mvn test'
          }
      }
      stage("Package"){
          steps{
              echo 'Package: step 3'
              sh 'mvn package -DskipTests'
          }
      }
  }

  post{
    always{
        echo 'This pipeline is completed..'
    }
  }
}
