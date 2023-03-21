pipeline {

  agent any

  parameters {
    string(name: 'COMPONENT', defaultValue: '', description: 'Component')
    string(name: 'APP_VERSION', defaultValue: '', description: 'App Version')
  }

  stages {

    stage('Get Values file') {
      steps {
        dir('APP') {
          git branch: 'main', url: 'https://github.com/raghudevopsb70/${COMPONENT}.git'
        }
        dir('HELM') {
          git branch: 'main', url: 'https://github.com/raghudevopsb70/roboshop-helm-chart'
        }
      }
    }

    stage('Helm Deploy') {
      steps {
        sh 'helm upgrade -i ${COMPONENT} ./HELM -f APP/values.yaml --set-string image.tag="${APP_VERSION},ENV=prod,COMPONENT=${COMPONENT}"'
      }

    }


  }

  post {
    always {
      cleanWs()
    }
  }



}