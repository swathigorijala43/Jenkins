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
  stage('Build and Test') {
      steps {
        sh 'ls -ltr'
        sh 'cd spring-boot-app && mvn clean package' // build the project and create a JAR file
      }
    }
   stage('Build and Push Docker Image') {
      environment {
        DOCKER_IMAGE = "swathigorijala/java-practice:${BUILD_NUMBER}"
        // DOCKERFILE_LOCATION = "java-maven-sonar-argocd-helm-k8s/spring-boot-app/Dockerfile"
        REGISTRY_CREDENTIALS = credentials('docker-cred')
      }
      steps {
        script {
            sh 'cd spring-boot-app && docker build -t ${DOCKER_IMAGE} .'
            def dockerImage = docker.image("${DOCKER_IMAGE}")
            docker.withRegistry('https://index.docker.io/v1/', "docker-cred") {
                dockerImage.push()
            }
        }
      }
    }
  }
}

        
