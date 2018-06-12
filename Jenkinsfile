@Library("Reform")
import uk.gov.hmcts.Ansible
def ansibleApI = new Ansible(this, 'bar')
def ansibleWeb = new Ansible(this, 'bar_web')
lock('bar-demo-deploy') {
  try {
    node {
      onMaster {
        stage('Clear down workspace') {
          deleteDir()
        }
        stage('Checkout management configuration') {
          checkout scm
          dir('ansible-management') {
            git url: "https://github.com/hmcts/ansible-management", branch: "master", credentialsId: "jenkins-public-github-api-token"
          }
        }
        stage('Deploy API (Demo)') {
          ansibleApI.runDeployPlaybook('', 'demo')
        }
         stage('Deploy Web (Demo)') {
           ansibleWeb.runDeployPlaybook('', 'demo')
        }
      }
    }
  } catch (err) {
    notifyBuildFailure channel: '#bar-tech'
    throw err
  }
}
