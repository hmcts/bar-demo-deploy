@Library("Reform")
import uk.gov.hmcts.Ansible

def ansibleApI = new Ansible(this, 'bar')
def ansibleWeb = new Ansible(this, 'bar_web')

lock('bar-demo-deploy') {

  try {
    node {
      onMaster {
        stage('Deploy API (Demo)') {
          deleteDir()
          ansibleApI.runDeployPlaybook('', 'demo')
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
