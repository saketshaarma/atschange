pipeline {
	agent any
	parameters {
        choice(
            name: 'BRANCH',
            choices: 'master\nrelease/v5.1\nR5.0',
            description: 'Selct the branch to deploy to repective Airflow')
    }
	stages {
		stage ("SCM CHECKOUT") {
			steps {
				checkout([$class: 'GitSCM',
				branches: [[name: "${params.BRANCH}"]],
				doGenerateSubmoduleConfigurations: false,
				extensions: [], submoduleCfg: [],
				userRemoteConfigs: [[url: 'https://github.com/Juniper/contrail-dev-env.git']]])
			}
	}

	}
}
