pipeline {
    agent any
	stages {
	    stage('SCM') {
		    steps {
			    echo 'git clone project from GitHub repository'   
			}
		}
		stage('mobsf-scan') {
		    steps {
			    sh 'pip3 install mobsfscan'
				sh 'mobsfscan app/src/main/java/sg/vantagepoint/ --sarif --output mobsfscan-result.txt'
				archiveArtifacts artifacts: mobsfscan-result.txt, fingerprint: true
			}
		}
	}
}