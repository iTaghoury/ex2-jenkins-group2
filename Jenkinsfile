pipeline {
  agent any
  stages {
    stage('email') {
      steps {
        echo 'Hello!'
      }
    }
  }
  post {
    always {
      emailext body: 'Hello email!', to: 'idriss.taghoury@gmail.com', subject: '$PROJECT_NAME - Build # $BUILD_NUMBER - $BUILD_STATUS!', recipientProviders: [[$class: 'DevelopersRecipientProvider'], [$class: 'RequesterRecipientProvider']]
    }
  }
}
