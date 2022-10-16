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
          export ARGOCD_SERVER="10.4.6.10:32218"
          export ARGOCD_AUTH_TOKEN=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJhcmdvY2QiLCJzdWIiOiJhZG1pbjphcGlLZXkiLCJuYmYiOjE2NjU4Nzc3MDcsImlhdCI6MTY2NTg3NzcwNywianRpIjoiYzQ2ZTI2MzUtMjEzNy00MWQ5LWEzZDYtM2QwYzBhMGJhNzE2In0.EmyHWykoJfn7icGjtHxtKWhFYThJlNezItZum081oKY
          export ARGOCD_OPTS="--grpc-web --insecure"
          argocd app list
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
