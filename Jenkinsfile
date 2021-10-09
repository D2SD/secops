pipeline {
  environment { 
    ARGO_SERVER = '35.239.154.108:32100' 
    DEV_URL = 'http://35.239.154.108:30080/'
  }

  agent any 

  stages {
    stage('Compliance Scan') {
      steps{
        echo 'Packaging vote app with docker'
          script{
            def remote = [:]
            remote.name = "node-1"
            remote.host = "188.166.208.199"
            remote.allowAnyHosts = true

            withCredentials([sshUserPrivateKey(credentialsId: 'sshUser', keyFileVariable: 'identity', passphraseVariable: '', usernameVariable: 'userName')]) {
                remote.user = userName
                remote.identityFile = identity
                stage("SSH Steps Rocks!") {
                  sshCommand remote: remote, command: 'for i in {1..5}; do echo -n \"Loop \$i \"; date ; sleep 1; done'
                  sshCommand remote: remote, command: 'echo "inspec exec /root/linux-baseline/"'
              }
            }
          }
       }
    }
  }
}

