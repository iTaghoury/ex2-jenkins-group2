pipeline {
  agent any
  stages {
    stage('email') {
      steps {
        echo 'Hello!'
        slackSend message: "started ${env.JOB_NAME} ${env.BUILD_NUMBER} (<${env.BUILD_URL}|Open>)"
        emailext body: 'Hello email!', to: 'idriss.taghoury@gmail.com', subject: '$PROJECT_NAME - Build # $BUILD_NUMBER - $BUILD_STATUS!', recipientProviders: [[$class: 'DevelopersRecipientProvider'], [$class: 'RequesterRecipientProvider']]
      }
    }
  }
  post {
    success {
      slackSend message: "Finished ${env.JOB_NAME} ${env.BUILD_NUMBER} (<${env.BUILD_URL}|Open>)! Success!", color: "good"
    }
    failure {
      slackSend message: "Failed ${env.JOB_NAME} ${env.BUILD_NUMBER} (<${env.BUILD_URL}|Open>)!", color: "danger"
    }
  }
}
