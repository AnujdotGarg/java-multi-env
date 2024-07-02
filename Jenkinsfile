pipeline{
agent {
  label 'devServer'
}
tools {
  maven 'Java-Maven'
}

stages {
  stage('build') {
    steps {
        sh 'mvn clean package'
    }
    post {
    success {
        archiveArtifacts artifacts: '**/target/*.war'
            }
        }
    }
}
}