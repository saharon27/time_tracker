pipeline {
  agent any
  environment {
    scannerHome = tool 'SonarQube_Runner'
  }
  tools {
    maven 'Maven 3.6.3'
  }
  stages {
    stage('Get_Sources') {
      steps {
        git(url: 'https://github.com/saharon27/time_tracker.git', branch: 'master', credentialsId: 'saharon_github')
      }
    }

    stage('build && SonarQube analysis') {
      steps {
        echo 'Building Maven...'
        sh 'mvn -Dmaven.test.failure.ignore=true package'
        withSonarQubeEnv(credentialsId: 'SonarQube_Token', installationName: 'SonarQube') {
          sh 'mvn org.sonarsource.scanner.maven:sonar-maven-plugin:3.6.0.1398:sonar'
        }
      }
    }
/*   stage('SonarQube analysis') {
     steps {
      withSonarQubeEnv(credentialsId: 'SonarQube_Token', installationName: 'SonarQube') {
        sh 'mvn org.sonarsource.scanner.maven:sonar-maven-plugin:3.6.0.1398:sonar'
      }
     }
    }
*/
    stage('Publish war file to nexus') {
      steps{
        nexusPublisher nexusInstanceId: 'nexus_server', nexusRepositoryId: 'maven-releases', packages: [[$class: 'MavenPackage', mavenAssetList: [[classifier: '', extension: '', filePath: '/var/jenkins_home/workspace/time_tracker/web/target/time-tracker-web-0.3.1.war']], mavenCoordinate: [artifactId: 'time-tracker-parent', groupId: 'clinic.programming.time-tracker', packaging: 'pom', version: '0.3.1']]], tagName: 'time_tracker'
      }
    }
          
/*    stage('build && SonarQube analysis') {
            steps {
                withSonarQubeEnv('SonarQube') {
                        sh 'mvn clean install sonar:sonar'
                  sh "${scannerHome}/bin/sonar-scanner"
                    }
                  }
*/       
//                withSonarQubeEnv('SonarQube') {
//                    sh "${scannerHome}/bin/sonar-scanner"
//                }
//                timeout(time: 10, unit: 'MINUTES') {
//                   waitForQualityGate abortPipeline: true
//                }
  }
}
