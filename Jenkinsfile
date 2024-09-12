def COLOR_MAP = [
    'SUCCESS': 'good',
    'FAILURE': 'danger',
]
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
            echo 'slack noti'
            slackSend channel: '#pls',
            color: COLOR_MAP[currentBuild.currentResult],
            message: "*${currentBuild.currentResult}:* \n Job = ${env.JOB_NAME} \n Build no. = ${env.BUILD_NUMBER} \n Github Repo = ${env.GIT_URL} \n Branch = ${env.BRANCH_NAME} \n Commit = ${env.GIT_COMMIT} \n Build URL = ${env.BUILD_URL} \n Github push by = ${env.GIT_COMMITTER_NAME} \n Github push email = ${env.GIT_COMMITTER_EMAIL} \n Github push message = ${env.GIT_COMMIT_MESSAGE} \n Github push time = ${env.GIT_COMMIT_TIMESTAMP} \n Done!!"
        }
        success {
            echo 'Pipeline completed successfully.'
        }
        failure {
            echo 'Pipeline failed.'
        }
    }
}
