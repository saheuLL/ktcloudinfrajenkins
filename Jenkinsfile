pipeline {
  agent any
  stages {
    stage('git scm update') {
      steps {
        git url: 'https://github.com/saheuLL/ktcloudinfrajenkins.git', branch: 'main'
      }
    }
    stage('delivery and deployment using k8s') {
      steps {
        sh '''
        ansible master -m shell -a "kubectl --kubeconfig=/etc/kubernetes/admin.conf get no"
        docker build -t saheul/ktcloudinfra:0727 .
        echo "############ Build finish"
        ansible master -m copy -a "src=/var/lib/jenkins/ktcloudinfrajenkins/deploy.yml  dest=/root/deploy.yml"
        echo "############ Copy finish"
        ansible master -m shell -a "kubectl --kubeconfig=/etc/kubernetes/admin.conf apply -f deploy.yml"        
        '''
      }
    }
  }
}
