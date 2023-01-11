pipeline {
    agent any
    stages { 
        stage('SCM') { 
            agent { label 'linux-vmsonar' }
            steps {
                git url: 'https://github.com/SebPercheQA/shopizer-projet3-groupe1.git'
            }
        }
        stage('build && SonarQube analysis') {
            agent { label 'linux-vmsonar' }
            steps {
                withSonarQubeEnv('My SonarQube Server') {
                    // Optionally use a Maven environment you've configured already
                    withMaven(maven:'maven3.6_local_VMagent') {
                        sh 'mvn clean package sonar:sonar'
                    }
                }
            }
        }
        stage("Quality Gate") {
            agent { label 'linux-vmsonar' }
            steps {
                timeout(time: 1, unit: 'HOURS') {
                    // Parameter indicates whether to set pipeline to UNSTABLE if Quality Gate fails
                    // true = set pipeline to UNSTABLE, false = don't
                    waitForQualityGate abortPipeline: true
                }
            }
        }
    }
}
