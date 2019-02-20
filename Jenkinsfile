#!groovy
try{
properties([buildDiscarder(logRotator(artifactDaysToKeepStr: '', artifactNumToKeepStr: '', daysToKeepStr: '', numToKeepStr: '5'))])

/*node('slave1') {*/
/*node (label: 'slave1') {*/
node('master'){

  cleanWs notFailBuild: true
  currentBuild.result = "SUCCESS"
  
  
  stage('Checkout'){

     checkout scm
  }
  */
  
  stage('checkout'){
     git credentialsId: 'bc32cfee-9364-4d7e-89f1-692273932b1e', url: 'https://github.com/jayaramsv/maven-standalone-application.git''
  }
  
  stage('build'){
     if(isUnix()){
     sh 'mvn deploy'
      }
      else{
       bat 'mvn deploy'   
      }
  }
   
 
 
 stage('sonarqubereport'){
     if(isUnix()){
     sh 'mvn sonar:sonar'
      }
      else{
       bat 'mvn sonar:sonar'   
      }
  }
  
  
  stage('DeployAppIntoTomcat'){
     if(isUnix()){
	  sh 'echo "Starting deployment"'
      sh 'cp %WORKSPACE%/target/*.war C:/apache-tomcat-9.0.14/apache-tomcat-9.0.14/webapps/'
      sh 'echo "Deployment done successfully"'
	  }
      else{
       bat 'echo windows'   
	   bat label: '', script: '''echo "start tomcat copy"
copy %WORKSPACE%\\target\\*.war C:\\apache-tomcat-9.0.14\\apache-tomcat-9.0.14\\webapps\\
echo "deploy the tomcat"'''
      }
  }
  
  	stage('emailnotification'){
  	      mail  to: 'devopstrainingblr@gmail.com', cc: 'devopstrainingblr@gmail.com', bcc: 'devopstrainingblr@gmail.com',from: 'devopstrainingblr@gmail.com', replyTo: 'devopstrainingblr@gmail.com',             subject: 'env.PROJECT_NAME - Build # env.BUILD_NUMBER - env.BUILD_STATUS' ,body: 'Buid Done '
  
    
  	   }
	  }catch(error){
         currentBuild.result = "FAILURE"

             mail body: "project build error is here: ${env.BUILD_URL}" ,
             from: 'devopstrainingblr@gmail.com',
             replyTo: 'mithunreddytechnologies@gmail.com',
             subject: 'project build failed',
             to: 'mithunreddytechnologies@gmail.com'

         throw err
	     throw error
	  }
  
}



cp $WORKSPACE/target/*.war /Users/bhaskarreddyl/BhaskarReddyL/Softwares/Running/apache-tomcat-9.0.12/mithunapps/

echo $WORKSPACE

/Users/bhaskarreddyl/.jenkins/workspace/pipeline-job-scriptedway















