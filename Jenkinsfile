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
                git branch: 'main', url: 'https://github.com/jahid28/portfolio.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                echo 'Installing npm dependencies...'
                sh 'npm install'
            }
        }

        // stage('Run Tests') {
        //     steps {
        //         echo 'Running tests...'
        //         sh 'npm test'
        //     }
        // }

        stage('Build App') {
            steps {
                echo 'Building the application...(pls run this time2)'
                sh 'npm run build'
            }
        }

        stage('Deploy to /var/www/html') {
            steps {
                script {
                    // Assuming Jenkins runs on the same EC2 instance
                    sh 'sudo cp -r build/* /var/www/html/'
                }
            }
        }

    }

    

    post {
        always {
            echo 'slack noti'
            slackSend channel: '#pls',
            color: COLOR_MAP[currentBuild.currentResult],
            message: "*${currentBuild.currentResult}:* \n Job = ${env.JOB_NAME} \n Build no. = ${env.BUILD_NUMBER} \n Github Repo = ${env.GIT_URL} \n React check is done!!"
        }
        success {
            echo 'Pipeline completed successfully.'
        }
        failure {
            echo 'Pipeline failed.'
        }
    }
}
