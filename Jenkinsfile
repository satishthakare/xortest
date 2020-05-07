
node {
   // This is to demo github action	
      def sonarUrl = 'sonar.host.url=http://10.20.14.81:9000/'
 
   stage('SCM Checkout'){
    // Clone repo
	git branch: 'master', 
	credentialsId: 'github', 
	url: 'https://github.com/satishthakare/xortest'
   
   }
   
    stage('SonarQube Analysis') {
        def mvnHome =  tool name: 'Maven 3', type: 'maven'
        withSonarQubeEnv('sonar6') { 
          sh "${mvnHome}/bin/mvn sonar:sonar"
        }
    }
	   
	 //  withCredentials([string(credentialsId: 'admin', variable: 'sonarToken')]) {
        //def sonarToken = "sonar.login=${sonarToken}"
        // sh "${mvn} sonar:sonar -D${sonarUrl}  -D${sonarToken}"
	// }
      
 //   }
   
	
   stage('Compile Package'){
	   // Build using maven
	   def mvn = tool (name: 'Maven 3', type: 'maven') + '/bin/mvn'
	   sh " ${mvn} package "
   }
   
   stage('deploy-dev'){
     def tomcatDevIp = '10.20.14.81'
	   def tomcatHome = '/opt/tomcat8/'
   def webApps = tomcatHome+'webapps/'
	   def tomcatStart = "${tomcatHome}bin/startup.sh"
	   def tomcatStop = "${tomcatHome}bin/shutdown.sh"
	   
   sshagent (credentials: ['varun2882']) {
	      sh "scp -o StrictHostKeyChecking=no target/myweb*.war varun2882@${tomcatDevIp}:${webApps}myweb.war"
        sh "ssh varun2882@${tomcatDevIp} ${tomcatStop}"
		  sh "ssh varun2882@${tomcatDevIp} ${tomcatStart}"
      }
  }
   //stage('Email Notification'){
	//	mail bcc: '', body: """Hi Team, You build successfully deployed
	//	                       Job URL : ${env.JOB_URL}
	//						   Job Name: ${env.JOB_NAME}

//Thanks,
//DevOps Team""", cc: '', from: '', replyTo: '', subject: "${env.JOB_NAME} Success", to: 'satishthakare0309@gmail.com'
   
//   }
}

