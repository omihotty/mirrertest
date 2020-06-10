node{
  stage('SCM Checkout'){
    git 'https://github.com/omihotty/jenk.git'  
  }

  stage('SonarQube'){
    def mvnHome = tool name: 'maven', type: 'maven'
    withSonarQubeEnv('sonar-server'){
      sh "${mvnHome}/bin/mvn sonar:sonar"
    }
  }

    stage("Quality Gate Statuc Check"){
          timeout(time: 1, unit: 'HOURS') {
              def qg = waitForQualityGate()
              if (qg.status != 'OK') {
                  emailext body: 'Build is Fail', subject: 'This Build has failed', to: 'singh.88omkar@gmail.com' 
              }
          }
      }    

  stage('Email Notification'){
     emailext body: 'this is only for testing purpose', subject: 'Hi this is for testing purpose', to: 'singh.88omkar@gmail.com'  
  }

}