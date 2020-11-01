pipeline {
  agent {
    kubernetes {
      label 'runner'
      idleMinutes 5
      yamlFile 'build-pod.yaml'  
      defaultContainer 'python'  
    }
  }

  environment {
      DOCKERHUB_PW = credentials('docker-hub-login')
  }
  
  stages {
      stage('Python runner testing') {
          steps {
              sh 'python -V'
          }
      }

      stage('Build and push Docker Im') {
          steps {
            container('docker') {  
              sh "docker build -t kanchimo/python-simple-app:$BUILD_NUMBER ."
              sh "docker login -u kanchimo -p $DOCKERHUB_PW"
              sh "docker push kanchimo/python-simple-app:$BUILD_NUMBER"
            }
          }
      }
  }
}
