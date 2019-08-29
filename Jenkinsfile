pipeline{
  agent{
    label { label 'itcloudconfig' 
    }
  }
  stages {
      stage ('TestCase1'){
      steps{
           echo 'Verifying LastReboot' 
           // Test Case -- Verifying the Server Last Reboot should Match the Current Date
           sh '~/scripts/Testcases/verifylastreboot.sh'
           
          }
      }
      stage ('TestCase2'){
      steps{
           echo 'Verifying Patchlog'
            // Check whether any security Updates Installed
            sh '~/scripts/Testcases/checkyumlog.sh'
           
      }
  }
    
    }
  post {
    success {
                echo 'Tests Passed'
           mail to: 'bramireddy@idirect.net',
             subject: "Change Completed Succesfully ",
             body: "Security Patching to ERP Servers -- (1 hr. Service disruption anticipated to ERP  Integration Application) "
    }
     failure {
        //build job: 'oraclestop', propagate: true, wait: false
       mail to: 'bramireddy@idirect.net',
             subject: "Test Failed Please check something is not Right : ${currentBuild.fullDisplayName}",
             body: "Test Failed Please check something is not Right  ${env.BUILD_URL}/consoleText"
       from : 'noreply@jenkins.com'
    }
  }
}
