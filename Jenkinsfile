node {
   
   stage('Code Checkout') { 
     git credentialsId: 'githubID', url: 'https://github.com/itrainbatman/maven-examples.git'
     
    }
   stage('Build') {
    withMaven(jdk: 'jdk-11', maven: 'Maven-3.6.0') {
      sh 'mvn clean compile'
      }
    }
   stage('Unit Test run') {
    withMaven(jdk: 'jdk-11', maven: 'Maven-3.6.0') {
     sh 'mvn test'
      } 
    }
   stage('Sonarqube analysis'){
      def scannerHome = tool 'javascanner';
   withSonarQubeEnv(credentialsId: 'ItrainSonar') {
    withMaven(jdk: 'jdk-11', maven: 'Maven-3.6.0') {
    sh 'mvn sonar:sonar' 
      }
     }
    }
  stage("Quality Gate"){
          timeout(time: 1, unit: 'HOURS') {
              def qg = waitForQualityGate()
              if (qg.status != 'OK') {
                  error "Pipeline aborted due to quality gate failure: ${qg.status}"
              }
          }
    }
   stage('Package to Jfrog') {
    withMaven(jdk: 'jdk-11', maven: 'Maven-3.6.0') {
     sh 'mvn package'
      }
    }
   
   stage('Deploy to Dev') {
     
    }
   stage('Automation Testing') {
     
    }
   stage('Deploy to Test') {
     
    }
   stage('Smoke Testing') {
     
    }
   stage('Deploy to Prod') {
     
    }
   stage('Acceptance Testing') {
     
    }
}
