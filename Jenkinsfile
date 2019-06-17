pipeline {
	agent any
	stages {
		stage ("SCM CHECKOUT") {
			steps {
				checkout([$class: 'GitSCM',
				branches: [[name: "${params.BRANCH}"]],
				doGenerateSubmoduleConfigurations: false,
				extensions: [], submoduleCfg: [],
				userRemoteConfigs: [[url: 'https://github.com/Juniper/contrail-dev-env.git']]])
				
				def checkoutDetails = checkout scm: newScm, poll: false, changelog: false
				echo "checkout scm returned SHA = ${checkoutDetails.GIT_COMMIT}"
			}
	}
	}
}


def getCommitSha(){
	return sh(returnStdout: true, script: 'git rev-parse HEAD')
}
