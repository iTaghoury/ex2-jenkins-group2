pipeline {
  agent any
  stages {
    stage('email') {
      steps {
        echo 'Hello!'
        slackSend message: "started ${env.JOB_NAME} ${env.BUILD_NUMBER} (<${env.BUILD_URL}|Open>)"
        emailext body: '$DEFAULT_CONTENT', to: 'idriss.taghoury@gmail.com', subject: '$DEFAULT_SUBJECT', recipientProviders: [[$class: 'DevelopersRecipientProvider'], [$class: 'RequesterRecipientProvider']]
      }
    }
  }
  post {
    always {
      echo "this will always be logged"
    }
    success {
      slackSend message: "Finished ${env.JOB_NAME} ${env.BUILD_NUMBER} (<${env.BUILD_URL}|Open>)! Success!", color: "good"
    }
    failure {
      slackSend message: "Failed ${env.JOB_NAME} ${env.BUILD_NUMBER} (<${env.BUILD_URL}|Open>)!", color: "danger"
    }
  }
}
