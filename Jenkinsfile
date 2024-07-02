pipeline{
agent {
  label 'devServer'
}
stages {
  stage('build') {
    steps {
        sh 'mvn clean package'
    }
  }

}
