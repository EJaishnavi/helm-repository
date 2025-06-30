pipeline {
  agent any

  environment {
    KUBECONFIG = '/var/lib/jenkins/minikube-config'  // Update as per your EC2 path
    RELEASE_NAME = 'myapp'
    CHART_PATH = 'myapp'
    NAMESPACE = 'dev'
  }

  stages {
    stage('Checkout Code') {
  steps {
    git branch: 'main',
        url: 'https://github.com/EJaishnavi/helm-repository.git'
  }
}

    stage('Helm Install') {
      steps {
        sh '''
          helm upgrade --install $RELEASE_NAME $CHART_PATH --namespace $NAMESPACE --create-namespace
          kubectl get all -n $NAMESPACE
        '''
      }
    }
stage('Verify Deployment') {
      steps {
        sh '''
          echo "Checking resources in namespace: $NAMESPACE"
          kubectl get pods -n $NAMESPACE
          kubectl get svc -n $NAMESPACE
        '''
      }
    }
  }
post {
    always {
      echo 'Post-build actions complete.'
    }
  }
}
