@Library("Reform")
import uk.gov.hmcts.Ansible

def ansible = new Ansible(this, 'bar')

lock('bar-demo-deploy') {

  try {
    node {
      onMaster {
        stage('Deploy (Demo') {
          deleteDir()
          ansible.runDeployPlaybook('', 'demo')
        }
      }
    }
  } catch (err) {
    notifyBuildFailure channel: '#bar-tech'
    throw err
  }
}