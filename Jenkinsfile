pipeline{
agent {
  label 'devServer'
}

tools {
  maven 'Java-Maven'
}
environment {
  dev = "non-production enviroment for dev and test, running on devServer"
  prod = "production env running on prodServer"
}
parameters {
  choice choices: ['Development', 'Production'], name: 'deploy-env'
}

stages {
  stage('build') {
    steps {
        sh 'mvn clean package'
        echo "$dev"
    }

        }
    stage('test')
    {
      parallel{
        stage('testA'){
          steps{
            echo "test A"
          }
        }
        stage('testB'){
          steps{
            echo "test B"
          }
        }
      post {
      success {
        archiveArtifacts artifacts: '**/target/*.war'
            }
          }
        }
      }
    }
  }