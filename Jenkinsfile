pipeline {
	environment {
	branch_name='v5.1'
	image_name='tungstenfabric/developer-sandbox'
	image_tag='r5.1'
	}
	agent any
	stages {
		stage ("SCM CHECKOUT") {
			steps {
				checkout([$class: 'GitSCM',
						branches: [[name: '*/${branch_name}']],
						doGenerateSubmoduleConfigurations: false,
						extensions: [], submoduleCfg: [],
						userRemoteConfigs: [[url: 'https://github.com/Juniper/contrail-dev-env.git']]])
			}
		stage ("Build Sandbox Image") {
			steps {
			sh label: '',
			script: 'cd container; docker build --build-arg BRANCH=master --no-cache --tag ${image_name}:${image_tag} .'
			}
		}
	}
}
}
