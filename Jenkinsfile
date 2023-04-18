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
    stage('jira-test') {
      steps {
        echo 'Starting jira-test...'
        script {
          def newIssue =  [
                fields: [
                  project: ['key': 'JEN'],
                  summary: 'New JIRA issue created with Jenkins',
                  description: 'Hello from Jenkins!',
                  issueType: [name: 'Story']
                ]
              ]
          jiraNewIssue issue: newIssue, site: "iTaghoury's Site"
        }
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
