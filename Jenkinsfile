pipeline {
  agent {
    kubernetes {
      idleMinutes 5
      yamlFile 'agent.yaml'  
      defaultContainer 'python'  
    }
  }

  environment {
      DOCKERHUB_PW = credentials('docker-passwd')
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
              sh "docker build -t trongthongvo/python-simple-app:$BUILD_NUMBER ."
              sh "docker login -u trongthongvo -p $DOCKERHUB_PW"
              sh "docker push trongthongvo/python-simple-app:$BUILD_NUMBER"
            }
          }
      }
  }
}
