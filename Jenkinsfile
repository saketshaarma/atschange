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
			}
	}
		stage ("Sandbox Image"){
			steps {
			sh label: '',
			script: 'cd container; \
			docker build --build-arg BRANCH=master --no-cache --tag tungstenfabric/developer-sandbox:r5.1 .'
			}
		
		}
		
		stage ("Container Orchestration"){
			steps {
				sh label: '',
				script: ' ./startup.sh -i tungstenfabric/developer-sandbox -t r5.1'
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
		
		stage ("Build Step make sync") {
			steps {
				sh label: '',
				script: ' docker exec contrail-developer-sandbox bash -c \'set -x; \
				cd /root/contrail-dev-env; \
				make sync; \
				make fetch_packages; \
				make setup; \
				make dep; \
				export SRCVER=r5.1; \
				export BUILDTAG=1; \
				make rpm;\''
			
			}
		}

	}
}


def getCommitSha(){
	return sh(returnStdout: true, script: 'git rev-parse HEAD')
}
