pipeline {
  agent any
  stages {
    stage('Get_Sources') {
      steps {
        git(url: 'git@github.com:saharon27/time_tracker.git', branch: 'master')
      }
    }

    stage('Build_Source') {
      steps {
        echo 'Building Maven...'
      }
    }

  }
}