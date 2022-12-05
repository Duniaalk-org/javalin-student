pipeline {

  options {
    ansiColor('xterm')
  }

  agent {
    kubernetes {
      yamlFile 'builder.yaml'
    }
  }

stages {
       
    stage('Checkout SCM') {
      steps {
        container('git') {
          git url: 'https://github.com/Duniaalk-org/javalin-student',
          branch: 'master'
        }
      }
    }
  stage('Build SW'){
      steps {
        container('maven'){
          sh 'mvn -Dmaven.test.failure.ignore=true clean package'
        }
      }
    }
    stage('Kaniko Java Build & Push Image') {
      steps {
        container('kaniko') {
          script {
            sh '''
            /kaniko/executor --dockerfile `pwd`/Dockerfile \
                             --context `pwd` \
                             --destination=duniaalk/hello-kaniko
            '''
          }
        }
      }
    }   

    
  }
}
