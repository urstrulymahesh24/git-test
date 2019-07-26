pipeline {
    agent any
    stages {
        stage('One') {
                steps {
                        echo 'Hi, this is Zulaikha from edureka'
			
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
                        agent {
                                docker {
                                        reuseNode false
					image 'ubuntu'
                                        }
			}
				steps {
					echo 'Running the integration test..'
				}
                               
		
			}
	    stage('slack notification') { 
		     steps{
           slackSend channel: 'rivet-jenkins', 
           color: 'red', iconEmoji: '', 
           message: 'Slack', teamDomain: 'kaay', 
           tokenCredentialId: 'Jenkins-slack', 
           username: 'mahesh'
		     }
       }

post {
       // only triggered when blue or green sign
       success {
           slackSend 
       }
       // triggered when red sign
       failure {
           slackSend 
       }
       // trigger every-works
       always {
           slackSend 
       }
}
        }
    }
}
}
