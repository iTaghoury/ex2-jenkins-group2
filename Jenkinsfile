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
                  issuetype: ['name': 'Story']
                ]
              ]
          jiraNewIssue issue: newIssue, site: "iTaghoury's Sit"
        }
      }
    }
  }
  post {
    success {
      slackSend message: "Finished ${env.JOB_NAME} ${env.BUILD_NUMBER} (<${env.BUILD_URL}|Open>)! Success!", color: "good"
    }
    failure {

      script {
          def failIssue =  [
                fields: [
                  project: ['key': 'JEN'],
                  summary: "Build ${env.BUILD_NUMBER} $BUILD_STATUS",
                  description: "Something went wrong! Build ${env.BUILD_NUMBER} failed",
                  issuetype: ['name': 'Bug']
                ]
              ]
          jiraNewIssue issue: failIssue, site: "iTaghoury's Site"
        }

      slackSend message: "Failed ${env.JOB_NAME} ${env.BUILD_NUMBER} (<${env.BUILD_URL}|Open>)!", color: "danger"
    }
  }
}
