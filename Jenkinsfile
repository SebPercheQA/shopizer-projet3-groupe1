pipeline {
  agent { node { label 'linux-vmsonar' } } {
    stages {
        stage('SCM') {
            steps {
                git url: 'https://github.com/SebPercheQA/shopizer-projet3-groupe1.git'
            }
        }
        stage('build && SonarQube analysis') {
            steps {
                withSonarQubeEnv('My SonarQube Server') {
                    // Optionally use a Maven environment you've configured already
                    withMaven(maven:'maven3.6_local_VMagent') {
                        sh 'sudo mvn clean verify sonar:sonar \
                            -Dsonar.projectKey=shopizerquality \
                            -Dsonar.host.url=http://192.168.102.142:9000 \
                            -Dsonar.login=a831ae73f120379d1280433a62d5665be38a87af'
                    
                    }
                }
            }
        }
        stage("Quality Gate") {
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
}
