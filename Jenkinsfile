def COLOR_MAP = [
    'SUCCESS': 'good',
    'FAILURE': 'danger',
]
pipeline {
    agent any  // Runs the pipeline on any available agent

    stages {
        stage('Cloning') {
            steps {
                echo 'Cloning from github...'
                git branch: 'main', url: 'https://github.com/jahid28/jenkins_test.git'
            }
        }

    }

    post {
        always {
            echo 'slack noti'
            slackSend channel: '#pls',
            color: COLOR_MAP[currentBuild.currentResult],
            message: "*${currentBuild.currentResult}:* \n Job = ${env.JOB_NAME} \n Build no. = ${env.BUILD_NUMBER} \n Github Repo = ${env.GIT_URL} \n Checking of new push is done!!"
        }
        success {
            echo 'Pipeline completed successfully.'
        }
        failure {
            echo 'Pipeline failed.'
        }
    }
}
