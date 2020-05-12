
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
     def tomcatDevIp = '10.20.14.183'
	   def tomcatHome = '/opt/tomcat/'
   def webApps = tomcatHome+'webapps/'
	   def tomcatStart = "${tomcatHome}bin/startup.sh"
	   def tomcatStop = "${tomcatHome}bin/shutdown.sh"
	   
   sshagent (credentials: ['centos']) {
	      cat remote_script.sh | sshpass -p centos ssh -T -o StrictHostKeyChecking=no centos@10.20.14.183:${webApps}myweb.war"
	      // sh "scp -o StrictHostKeyChecking=no target/myweb*.war centos@${tomcatDevIp}:${webApps}myweb.war"
        sh "ssh centos@${tomcatDevIp} ${tomcatStop}"
		  sh "ssh centos@${tomcatDevIp} ${tomcatStart}"
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

