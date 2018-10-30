pipeline {
	agent { label 'slave1' }
    stages {
        stage('One') {
                steps {
                        echo 'clone git repo'
                        git(
                                url: 'https://wwwin-github.cisco.com/webex-iaas/ansible-tower.git',
                                credentialsId: 'cisco_cec',
                                branch: "master"
                        )
                        sh '''
                          pip install ansible-lint
                          pip install ansible
                          ansible-playbook Ansible-Jenkins/createTestVM_Linting.yml
                        '''
                }
        }
	    stage('Two'){
		steps {
			input('Do you want to proceed?')
        }
	    }
        stage('Three') {
                when {
                        not {
                                branch "master"
                        }
                }
                steps {
			echo "Hello"
                        }
        }
        stage('Four') {
                parallel {
                        stage('Unit Test') {
                                steps{
                                        echo "Running the unit test..."
                                }
                        }
                        stage('Integration test') {
				steps {
					echo 'Running the integration test..'
				}
			}  }
        }
    }
}

