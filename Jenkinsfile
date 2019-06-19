def CONTRAIL_VERSION="r5.1"
def BRANCH="R5.1"
image_name="tungstenfabric/developer-sandbox"
image_tag="r5.1"
pipeline {
	agent any
	stages {
		stage ("SCM CHECKOUT") {
			steps {
				git branch: "${BRANCH}", url: 'https://github.com/Juniper/contrail-dev-env.git'
			}
	}
	}
}
