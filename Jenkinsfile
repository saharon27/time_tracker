pipeline {
  agent any
  tools {
    maven 'Maven 3.6.3'
  }
  stages {
    stage('Get_Sources') {
      steps {
        git(url: 'git@github.com:saharon27/time_tracker.git', branch: 'master', credentialsId: 'saharon_github_token')
      }
    }

    stage('Build_Source') {
      steps {
        echo 'Building Maven...'
        sh 'mvn -Dmaven.test.failure.ignore=true install'
      }
    }

  }
}
