pipeline{
agent any
tools{
 maven  "maven"
}

 
 triggers{
 githubPush()
 }
 
 options{
 timestamps()
 buildDiscarder(logRotator(artifactDaysToKeepStr: '', artifactNumToKeepStr: '3', daysToKeepStr: '', numToKeepStr: '3'))
 }
 
 stages{
   stage('CheckoutCode')
   {
   steps{
    git credentialsId: 'f59a3ecc-6200-4cb2-9b6e-3d0f96363e78', url: 'https://github.com/rajeshwarayya/sample.git'
   }
   }
 
   
    stage('Build')
    {
   steps{
    sh "mvn clean package"
   }
   }
   
   stage('ExecuteSonarQubeReportintotheSonarQubeServer')
    {
   steps{
    sh "mvn sonar:sonar"
   }
   }
   
   stage('DeployApplicationintotheTomcatServer')
    {
   steps{
       
    sshagent(credentials: ['ec9e677c-e96d-43b9-9b70-37993ba96bef'], ignoreMissing: true) {
    sh "scp -o StrictHostKeyChecking=no target/my-app-1.0-SNAPSHOT.jar ec2-user@65.2.5.151:/opt/tomcat8/webapps"
}   
       
   }
   
   } 
}
}
