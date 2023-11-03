pipeline {
  agent {
    docker { 
      image 'abhishekf5/maven-abhishek-docker-agent:v1' 
      args '--user root -v /var/run/docker.sock:/var/run/docker.sock' // mount Docker socket to access the host's Docker daemon
    }
  }
  stages {
    stage('checkout') {
      steps {
        sh 'echo passed'
        git branch: 'main', url: 'https://github.com/swathigorijala43/Jenkins.git'
      }
    }
  }
  stage('Build and Test') {
      steps {
        sh 'ls -ltr'
        //sh 'mvn clean package' // build the project and create a JAR file
      }
    }
}

        
