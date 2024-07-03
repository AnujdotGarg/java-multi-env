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
  choice choices: ['dev', 'prod'], name: 'deploy-env'
}

stages {
  stage('build') {
    steps {
        sh 'mvn clean package DskipTest=true'
        echo "$dev"
    }
  }
  stage('test')
  {
    parallel {
      stage('testA'){
        agent { label 'devServer' }
        steps{
          echo "test A"
          sh 'mvn test'
        }
      }
      stage('testB'){
        agent { label 'prodServer'}
        steps{
          echo "test B"
          sh 'mvn test'
          }
        }
      }
    post {
    success {
      dir("webapp/target/")
      {
      stash name: "java-hw-app", includes: "*.war"
          }
        }
      }
    }
  stage('deploy_dev')
  {
    when { expression {params.deploy_env == 'dev'}
    beforeAgent = true
    }
    agent { label 'devServer'}
    steps{
      dir("/var/www/html")
      {
        unstash "java-hw-app"
      }
      sh """
      cd /var/www/html
      jar -xvf webapp.war
      """
      }
    }  
  }
}