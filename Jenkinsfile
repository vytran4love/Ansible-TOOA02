def COLOR_MAP = ['SUCCESS': 'good', 'FAILURE': 'danger', 'UNSTABLE': 'danger', 'ABORTED': 'danger']
pipeline {
	agent any


  options {
    ansiColor('xterm')
    timestamps()
    buildDiscarder(logRotator(daysToKeepStr: '5'))
  }

	environment {
    ANSIBLE_HOST_KEY_CHECKING = 'False'
    ANSIBLE = '/usr/bin/ansible'
	}

	stages{
		stage("Run ansible command"){
			steps {
				sh """
          ansible-inventory -i lab_example/hosts --graph
          ${ANSIBLE}  -i lab_example/hosts host_name\
	    			-e ansible_ssh_user=ubuntu \
						-e ansible_ssh_private_key_file=~/.ssh/remote.pem \
						--become  \
						-m shell \
						-a "pwd && whoami"
				"""
			}
		}
	}

	post {
    failure {
      slackSend (
      	color: COLOR_MAP[currentBuild.currentResult],
        channel: '#general',
        message: "*`${currentBuild.currentResult}`*: *${env.JOB_NAME}*, \nRun in ${currentBuild.durationString} - <${env.BUILD_URL}|Go to this job>")
    }
  }
}

