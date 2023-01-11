// Powered by Infostretch 

timestamps {

node ('linux-vmshopizerjenkins') { 

	stage ('shopizer_packaging - Checkout') {
 	 checkout([$class: 'GitSCM', branches: [[name: '*/2.7.0']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: '', url: 'https://github.com/SebPercheQA/shopizer-projet3-groupe1']]]) 
	}
	stage ('shopizer_packaging - Build') {
 	
withEnv(["JAVA_HOME=${ tool '"+JDK+"' }", "PATH=${env.JAVA_HOME}/bin"]) { 
		// Maven build step
	withMaven(jdk: 'java8openJDK_VMagentShopizerJenkins', maven: 'maven3.6_local_VMagentShopizerJenkins') { 
 			if(isUnix()) {
 				sh "mvn clean package -Dmaven.test.skip=true " 
			} else { 
 				bat "mvn clean package -Dmaven.test.skip=true " 
			} 
 		} 
	}
}
	stage ('shopizer_testsUnitaires_codeAnalysisMetrics - Build') {
 	
withEnv(["JAVA_HOME=${ tool '"+JDK+"' }", "PATH=${env.JAVA_HOME}/bin"]) { 
		// Maven build step
	withMaven(jdk: 'java8openJDK_VMagentShopizerJenkins', maven: 'maven3.6_local_VMagentShopizerJenkins') { 
 			if(isUnix()) {
 				sh "mvn clean test
checkstyle:checkstyle
findbugs:findbugs
pmd:pmd " 
			} else { 
 				bat "mvn clean test
checkstyle:checkstyle
findbugs:findbugs
pmd:pmd " 
			} 
 		}
		// JUnit Results
		junit '**/target/surefire-reports/*.xml' 
	}
}
	stage ('shopizer_sonar - Build') {
 	
withEnv(["JAVA_HOME=${ tool '"+JDK+"' }", "PATH=${env.JAVA_HOME}/bin"]) { 

// Unable to convert a build step referring to "hudson.plugins.sonar.SonarRunnerBuilder". Please verify and convert manually if required. 
	}
}
}
}
