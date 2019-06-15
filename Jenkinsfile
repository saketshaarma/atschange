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
		stage ("Build Sandbox Image") {
			steps {
			sh label: '',
			script: 'cd container; docker build --build-arg BRANCH=master --no-cache --tag tungstenfabric/developer-sandbox:r5.1 .'
			}
		}
	}
}
