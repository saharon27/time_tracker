pipeline {
  agent any
  stages {
    stage('Get_Sources') {
      steps {
        git(url: 'git@github.com:saharon27/time_tracker.git', branch: 'master', credentialsId: 'saharon27')
      }
    }

    stage('Build_Source') {
      steps {
        echo 'Building Maven...'
      }
    }

  }
}