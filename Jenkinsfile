pipeline {
	agent any
	stages {
		stage ("SCM CHECKOUT FROM CONTRAIL REPO") {
			steps {
				git branch: 'v5.1', url: 'https://github.com/Juniper/contrail-dev-env.git'
			}
		}
	}
}
