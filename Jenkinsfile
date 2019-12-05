pipeline {
  agent any
  tools {
    maven 'Maven 3.6.3'
  }
  stages {
    stage('Get_Sources') {
      steps {
        git(url: 'https://github.com/saharon27/time_tracker.git', branch: 'master', credentialsId: 'saharon_github')
      }
    }

/*    stage('Build_Source') {
      steps {
        echo 'Building Maven...'
        sh 'mvn -Dmaven.test.failure.ignore=true install'
      }
    }
    stage('SonarQube analysis') {
      withSonarQubeEnv(credentialsId: 'SonarQube_Token', installationName: 'SonarQube') {
        sh 'mvn org.sonarsource.scanner.maven:sonar-maven-plugin:3.6.0.1398:sonar'
      }
    }
*/
    
    stage('build && SonarQube analysis') {
            steps {
                withSonarQubeEnv('SonarQube') {
                    withMaven(maven:'Maven 3.6.3') {
                        sh 'mvn clean package sonar:sonar'
                    }
                }
            }
        }
        stage("Quality Gate") {
            steps {
                timeout(time: 1, unit: 'HOURS') {
                    // Parameter indicates whether to set pipeline to UNSTABLE if Quality Gate fails
                    // true = set pipeline to UNSTABLE, false = don't
                    waitForQualityGate abortPipeline: true
                }
            }
        }
    
  }
}
