pipeline {
  agent {
    label "kube-agent"
  }
  
  environment {
    TAG = sh (script: "date +%y%m%d%H%M", returnStdout: true).trim()
  }
  
  stages {
    stage('Preparation') {
      steps {
        container('webapp-agent') {
          sh "echo App Version = $TAG"
        }
      }
    }
    stage('Update manifest') {
      steps {
        container('argocd') {
          sh """
          ls -la
          """
        }
      }
    }
/*
    stage('Test') {
      steps {
        container('webapp-agent') {
          sh "html5validator html/index.html"
        }
      }
      post {
        success {
           echo "Test Successful"
        }
        failure {
           echo "Test Failed"
        }
      }
    }
    
    stage("Build & Push Image"){
      steps{
        container('kaniko'){
          sh """
          /kaniko/executor --dockerfile `pwd`/Dockerfile --context `pwd` \
          --verbosity debug --destination docker.io/atwatanmalikm/webapp:$TAG
          """
        }
      }
    }

    stage("Update Manifest"){
      steps{
        container('kaniko'){
          sh """
          /kaniko/executor --dockerfile `pwd`/Dockerfile --context `pwd` \
          --verbosity debug --destination docker.io/atwatanmalikm/webapp:$TAG
          """
        }
      }
    }
*/
  }
}
