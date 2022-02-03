pipeline {

  agent { label 'kubepod' }

  stages {

    stage('Checkout Source') {
      steps {
        git url:'https://github.com/sajivesukumara/jenkins-playbook.git', branch:'main'
      }
    }

    stage('deploy using kubectl') {
      steps {
        container ('base') {
          sh '''
          kubectl apply -f nginx.yaml
          '''
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
