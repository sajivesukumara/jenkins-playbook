pipeline {

  agent { label 'kubepod' }

  stages {

    stage('Checkout Source') {
      steps {
        git url:'https://github.com/sajivesukumara/jenkins-playbook.git', branch:'main'
      }
    }
    
    stage('Deploy k8s App') {
      steps {
        script {
           kubernetesDeploy configs: 'nginx.yaml', kubeConfig: [path: ''], kubeconfigId: 'mykubeconfig', secretName: '', ssh: [sshCredentialsId: '*', sshServer: ''], textCredentials: [certificateAuthorityData: '', clientCertificateData: '', clientKeyData: '', serverUrl: 'https://']
        }
      }
    }
    
    stage('Deploy App') {
      steps {
        script {
          kubernetesDeploy(configs: "nginx.yaml", 
                           kubeconfigId: "mykubeconfig",
                           enableConfigSubstitution: false)
        }
      }
    }

  }

}
