pipeline{
  agent{
    label { label 'itcloudconfig' 
    }
  }
  stages {
      stage ('TestCase1'){
      steps{
           echo 'Verifying LastReboot' 
           sh '/home/jenkins/lastreboot.sh'
           sh '/home/jenkins/currentdate.sh'
           sh '/home/jenkins/verifylastreboot.sh'
           
          }
      }
      stage ('TestCase2'){
      steps{
           echo 'Verifying Patchlog'
            sh '/home/jenkins/patchlog.sh'
            sh '/home/jenkins/checkyumlog.sh patchlog'
           
      }
  }
    
    }
  }
  post {
    success {
                echo 'Tests Passed'
           mail to: 'bramireddy@idirect.net',
             subject: "Test Passed : ${currentBuild.fullDisplayName}",
             body: "Test Passed  ${env.BUILD_URL}/consoleText"
    }
     failure {
        mail to: 'bramireddy@idirect.net',
             subject: "Test Failed: ${currentBuild.fullDisplayName}",
             body: "Test  Failed for some reason  ${env.BUILD_URL}/consoleText"
    }
  }
}
}
