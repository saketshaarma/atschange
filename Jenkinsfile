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
				def commitHash = checkout(scm).GIT_COMMIT
			}
	}

	}
}
