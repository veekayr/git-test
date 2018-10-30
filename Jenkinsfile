pipeline {
	agent { label 'slave1' }
    stages {
        stage('One') {
                steps {
                        echo 'clone git repo'
                        git(
                                url: 'https://github.com/veekayr/AnsibleforTest.git',
                                credentialsId: '8edaf37d-5efc-46e8-893f-ab41ea1ca9ef',
                                branch: "master"
                        )
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

