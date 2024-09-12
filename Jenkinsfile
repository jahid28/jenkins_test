pipeline {
    agent any  // Runs the pipeline on any available agent

    stages {
        stage('Build') {
            steps {
                echo 'Building the application...'
            }
        }

        stage('Test') {
		    environment {
				myname = 'jahid'
		    }
            steps {
                echo "Running tests & name is ${myname}"
            }
        }

    }

    post {
        always {
            echo 'This will always run, regardless of the pipeline status.'
        }
        success {
            echo 'Pipeline completed successfully.'
        }
        failure {
            echo 'Pipeline failed.'
        }
    }
}
