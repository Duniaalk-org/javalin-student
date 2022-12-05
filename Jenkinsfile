podTemplate(yaml: '''
apiVersion: v1
kind: Pod
metadata:
     name: kaniko-pod
spec:
    containers:
      - name: maven
        image: maven:3.8.1-jdk-8
        command:
        - sleep
        args:
        - 99d
      - name: kaniko
        image: gcr.io/kaniko-project/executor:debug-539ddefcae3fd6b411a95982a830d987f4214251
        volumeMounts:
        - name: kaniko-secret
          mountPath: /kaniko/.docker
    restartPolicy: Never
    volumes:
      - name: kaniko-secret
        secret:
            secretName: dockercred
            items:
            - key: .dockerconfigjson
              path: config.json   
''') {
  node(POD_LABEL) {
    
    stage('Checkout SCM') {
      steps {
        container('git') {
          git url: 'https://github.com/Duniaalk-org/javalin-student',
          branch: 'master'
        }
      }
    }
       
    stage('Build Java Image & push') {
      container('kaniko') {
        stage('Build a Go project') {
          sh '''
            /kaniko/executor --dockerfile `pwd`/Dockerfile \
                             --context `pwd` \
                             --destination=duniaalk/hello-kaniko:1.0
          '''
        }
      }
    }

  }
}
