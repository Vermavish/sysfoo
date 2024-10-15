pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        echo 'Build: step 1'
        sh 'mvn compile'
      }
    }

    stage('Test') {
      parallel {
        stage('Test') {
          steps {
            echo 'Test: step 2'
            sh 'mvn test'
          }
        }

        stage('Validate') {
          steps {
            echo 'test Validation done'
            sleep 5
          }
        }

        stage('Regresss') {
          steps {
            echo 'Regress'
            sleep 10
          }
        }

      }
    }

    stage('Package') {
      steps {
        echo 'Package: step 3'
        sh 'mvn package -DskipTests'
      }
    }

  }
  tools {
    maven 'Maven 3.6.3'
  }
  post {
    always {
      echo 'This pipeline is completed..'
    }

  }
}