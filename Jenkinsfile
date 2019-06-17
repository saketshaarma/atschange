pipeline {
	agent any
	stages {
		stage ("SCM CHECKOUT") {
			steps {
				checkout([$class: 'GitSCM',
						branches: [[name: '*/master']],
						doGenerateSubmoduleConfigurations: false,
						extensions: [], submoduleCfg: [],
						userRemoteConfigs: [[url: 'https://github.com/Juniper/contrail-dev-env.git']]])
			}
	}

	}
}
