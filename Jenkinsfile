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

        docker.image('williamyeh/ansible:centos7').inside("--network 2-cd-platform_cd-in-practice") {
             checkout([$class: 'GitSCM', branches: [[name: "master"]], doGenerateSubmoduleConfigurations: false,
                       extensions: [[$class: 'RelativeTargetDirectory', relativeTargetDir: "env-conf"]], submoduleCfg: [],
                       userRemoteConfigs: [[url: "https://github.com/cd-in-practice/2-env-conf.git"]]])
             sh "ls -al"
             sh """
                ansible-playbook --syntax-check deploy/playbook.yaml -i env-conf/dev
                ansible-playbook -i env-conf/dev  deploy/playbook.yml
             """
           }
        
      }
}}}