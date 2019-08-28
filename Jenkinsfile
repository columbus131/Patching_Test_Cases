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
            //sh '/home/jenkins/patchlog.sh > patchlog'
            sh '/home/jenkins/checkyumlog.sh patchlog'
           
      }
  }
    
    }
  post {
    success {
                echo 'Tests Passed'
           mail to: 'bramireddy@idirect.net',
             subject: "Change Completed Succesfully Inform CAB : ${currentBuild.fullDisplayName}",
             body: "Change Completed Succesfully  ${env.BUILD_URL}/consoleText"
    }
     failure {
        //build job: 'oraclestop', propagate: true, wait: false
       mail to: 'bramireddy@idirect.net',
             subject: "Test Failed Please check something is not Right : ${currentBuild.fullDisplayName}",
             body: "Test Failed Please check something is not Right  ${env.BUILD_URL}/consoleText"
    }
  }
}
