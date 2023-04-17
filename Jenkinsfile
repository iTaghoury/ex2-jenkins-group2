pipeline {
  agent any
  stages {
    stage('email') {
      steps {
        echo 'Hello!'
        emailext body: 'Hello email!', to: 'idriss.taghoury@gmail.com'
      }
    }
  }
}
