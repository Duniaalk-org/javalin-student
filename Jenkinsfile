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
 
    
  }
}
