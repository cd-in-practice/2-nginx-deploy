pipeline{
  agent { label "docker"}
  environment{
    ANSIBLE_HOST_KEY_CHECKING = false
  }
  stages{
    stage("check nginx config"){
      steps{
        echo "verify nginx config"
      }
    }
    stage("deploy nginx"){
      steps{
        sh "ansible-playbook -i env-conf/dev  deploy/playbook.yml"
      }
}}}