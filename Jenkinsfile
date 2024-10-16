pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        echo 'Build: step 1'
        sh 'mvn compile'
      }
    }
    stage('Deploy to Dev') {
    when {

    beforeAgent true
    branch 'main'
    }
    agent any
    steps {
    echo 'Deploying to Dev Environment with Docker Compose'
    sh 'docker compose up -d'
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
      parallel {
        stage('Package') {
          steps {
            echo 'Package: step 3'
            sh 'mvn package -DskipTests'
          }
        }

        stage('Docker B&P') {
        when {
            beforeAgent true
            branch 'main'
            }
          agent any
          steps {
            script {
              docker.withRegistry('https://index.docker.io/v1/', 'dockerlogin')

              {
                def commitHash = env.GIT_COMMIT.take(7)
                def dockerImage = docker.build("vermavish/sysfoo:${commitHash}", "./")
                dockerImage.push()
                dockerImage.push("latest")
                dockerImage.push("dev")
              }
            }

          }
        }

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