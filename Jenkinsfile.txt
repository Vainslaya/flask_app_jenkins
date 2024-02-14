pipeline {
  agent any
  stages {
    stage('Git') {
      steps {
        git(url: 'https://github.com/Vainslaya/flask_app_jenkins.git', branch: 'main')
      }
    }

    stage('Build') {
      steps {
        sh 'docker build -t siilvance/jenkins_example .'
      }
    }

    stage('Docker Login') {
      steps {
        sh 'docker login -u siilvance -p dckr_pat_Rl_9tlFwhNhDOOlBJaACRDMa1uk'
      }
    }

    stage('Push') {
      steps {
        sh 'docker push siilvance/jenkins_example'
      }
    }

  }
}