// Define variable
def time_tracker_Image

pipeline {
  agent {
          kubernetes {
            label 'dockerPod'
            yaml """
              apiVersion: v1
              kind: Pod
              spec:
                containers:
                - name: docker
                  image: docker
                  command:
                  - cat
                  tty: true
                  volumeMounts:
                    - name: docker-sock
                      mountPath: '/var/run/docker.sock'
                - name: maven
                  image: maven:3.6.3-jdk-8-openj9
                  command:
                  - cat
                  tty: true
                  volumeMounts:
                    - name: docker-sock
                      mountPath: '/var/run/docker.sock'
                volumes:
                  - name: docker-sock
                    hostPath:
                      path: '/var/run/docker.sock'
                      type: File
              """
            }
        }
  environment {
    scannerHome = tool 'SonarQubeRunner'
  }
  tools {
    maven 'Maven 3.6.3'
  }
  
  stages {
    stage('docker container test') {
      steps{
        container('docker') {
          sh 'docker ps'
        }
      }
    }
/*    stage('Get_Sources') {
      steps {
        git(url: 'https://github.com/saharon27/time_tracker.git', branch: 'master', credentialsId: 'GitHub_Creds_HTTPS')
      }
    }

    stage('build && SonarQube analysis') {
      steps {
        echo 'Building Maven...'
        sh 'mvn -Dmaven.test.failure.ignore=true package'
        echo "Scanning with SonarQube..."
        withSonarQubeEnv(credentialsId: 'SonarQube_Token', installationName: 'SonarQube') {
          sh 'mvn org.sonarsource.scanner.maven:sonar-maven-plugin:3.6.0.1398:sonar'
        }
      }
    }*/
/*   stage('SonarQube analysis') {
     steps {
      withSonarQubeEnv(credentialsId: 'SonarQube_Token', installationName: 'SonarQube') {
        sh 'mvn org.sonarsource.scanner.maven:sonar-maven-plugin:3.6.0.1398:sonar'
      }
     }
    }
*/
/*    stage('Publish war file to nexus') {
      steps{
        echo "Publish war file to Nexus Maven-Releases repository..."
        nexusPublisher nexusInstanceId: 'nexus_server', nexusRepositoryId: 'maven-releases', packages: [[$class: 'MavenPackage', mavenAssetList: [[classifier: '', extension: 'war', filePath: '/home/jenkins/agent/workspace/time_tracker/web/target/time-tracker-web-0.3.1.war']], mavenCoordinate: [artifactId: 'time-tracker-parent', groupId: 'clinic.programming.time-tracker', packaging: 'war', version: '0.3.1']]]      
      }
    }

    stage('Dockerize App') {
      steps{
        container('docker') {
//        script{
//          time_tracker_Image = docker.build("time-tracker:0.3.1")
//        }
          //   customImage.push()

       // customImage.push('latest')
          echo "Creating Docker image..."
          sh 'docker build -f DockerFile -t sharon/time-tracker:0.3.1 .'
        }
      }
    }
    
    stage('Upload Docker to Nexus Repository') {
      steps{
        echo "Uploading Docker image to Nexus Repository..."
      }
    }*/
/*    post {
      success {
          mail to: 'team@example.com',
                  subject: "passed Pipeline: ${currentBuild.fullDisplayName}",
                  body: "Something is OK with ${env.BUILD_URL}"
        }
      failure {
          // notify users when the Pipeline fails
          mail to: 'team@example.com',
                  subject: "Failed Pipeline: ${currentBuild.fullDisplayName}",
                  body: "Something is wrong with ${env.BUILD_URL}"
        }
    }
*/    
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
