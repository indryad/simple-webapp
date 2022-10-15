pipeline {
  agent {
    label "kube-agent"
  }

    environment {
        version = 'v2'
    }

    stages {
        stage('Preparation') {
            steps {
              container('webapp-agent') {
                echo "App Version = ${version}"
              }
            }
        }

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

        stage("build-and-push=image"){
            steps{
              container('kaniko'){
                sh 'ls -lah; /kaniko/executor --dockerfile `pwd`/Dockerfile --context `pwd` --verbosity debug --destination docker.io/atwatanmalikm/webapp:test'
              }
            }
        }
    }
}
