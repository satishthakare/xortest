
//node {
   // This is to demo github action	
//   def sonarUrl = 'sonar.host.url=http://172.31.30.136:9000'
 //  def mvn = tool (name: 'maven3', type: 'maven') + '/bin/mvn'
   stage('SCM Checkout'){
    // Clone repo
	git branch: 'master', 
	credentialsId: 'github', 
	url: 'https://github.com/satishthakare/xortest'
   
   }
   
   //stage('Sonar Publish'){
//	   withCredentials([string(credentialsId: 'sonarqube', variable: 'sonarToken')]) {
   //     def sonarToken = "sonar.login=${sonarToken}"
     //   sh "${mvn} sonar:sonar -D${sonarUrl}  -D${sonarToken}"
	// }
      
//   }
   
	
   stage('Mvn Package'){
	   // Build using maven
	   def mvn = tool name: 'Maven 3.6.3', type: 'maven'
	   sh "${mvn}/bin/mvn package "
   }
   
//   stage('deploy-dev'){
   //    def tomcatDevIp = '172.31.28.172'
//	   def tomcatHome = '/opt/tomcat8/'
//   def webApps = tomcatHome+'webapps/'
//	   def tomcatStart = "${tomcatHome}bin/startup.sh"
//	   def tomcatStop = "${tomcatHome}bin/shutdown.sh"
	   
//	   sshagent (credentials: ['tomcat-dev']) {
//	      sh "scp -o StrictHostKeyChecking=no target/myweb*.war ec2-user@${tomcatDevIp}:${webApps}myweb.war"
//          sh "ssh ec2-user@${tomcatDevIp} ${tomcatStop}"
//		  sh "ssh ec2-user@${tomcatDevIp} ${tomcatStart}"
  //     }
  // }
   //stage('Email Notification'){
	//	mail bcc: '', body: """Hi Team, You build successfully deployed
	//	                       Job URL : ${env.JOB_URL}
	//						   Job Name: ${env.JOB_NAME}

//Thanks,
//DevOps Team""", cc: '', from: '', replyTo: '', subject: "${env.JOB_NAME} Success", to: 'satishthakare0309@gmail.com'
   
//   }
//}

