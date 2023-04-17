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
      slackSend "started ${env.JOB_NAME} ${env.BUILD_NUMBER} (<${env.BUILD_URL}|Open>)"
    }
  }
}
