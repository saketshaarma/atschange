def CONTRAIL_VERSION="r5.1"
def BRANCH="R5.1"
image_name="tungstenfabric/developer-sandbox"
image_tag="r5.1
pipeline {
	agent any
	stages {
		stage ("SCM CHECKOUT") {
			steps {
				checkout([$class: 'GitSCM',
				branches: [[name: "${BRANCH}"]],
				doGenerateSubmoduleConfigurations: false,
				extensions: [], submoduleCfg: [],
				userRemoteConfigs: [[url: 'https://github.com/Juniper/contrail-dev-env.git']]])
			}
	}
		stage ("Sandbox Image"){
			steps {
			sh label: '',
			script: "cd container; \
				docker build --build-arg BRANCH=master --no-cache --tag ${image_name}:${image_tag} ."
			}
		
		}
		
		stage ("Container Orchestration"){
			steps {
				sh label: '',
				script: " ./startup.sh -i ${image_name} -t ${image_tag}"
			}
		}
		stage ("Updating tpc.repo.template") {
			steps {
				sh label: '',
				script: '''cat <<EOF> tpc.repo.template
				[contrail-tpc]
				name=Third partiey for Contrail
                bayeurl=http://148.251.5.90/tpc-R5.1/
                enabled=1
                gpgcheck=0
                EOF'''
			
			}
		}
		stage ("Copying tpc.repo.template to container"){
			steps {
				sh label: '',
				script: 'docker cp tpc.repo.template contrail-developer-sandbox:/root/contrail-dev-env'
			
			}
		}
		
	}
}
