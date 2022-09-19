pipeline {
    agent any
    environment {
        DB_URL = 'mysql+pymysql://usr:pwd@host:<port>/db'
        DISABLE_AUTH = true
        AWS_ACCESS_KEY_ID = credentials('aws-access-key-id')
        AWS_SECRET_ACCESS_KEY = credentials('aws-access-secret-key')
    }
    stages {
        stage("Build") {
            steps {
                echo "Building the app..."
                sh '''
                    echo "This block contains multi-line steps"
                    ls -lh
                '''
                sh '''
                    echo "Database url is: ${DB_URL}"
                    echo "DISABLE_AUTH is ${DISABLE_AUTH}"
                    env
                '''
                echo "Running a job with build #: ${env.BUILD_NUMBER} on ${env.JENKINS_URL}"
            }
        }
        stage("Test") {
            steps {
                echo "Testing the app..."
            }
        }
        stage("Deploy") {
            steps {
                echo "Deploying the app..."
            }
        }
    }
    post {
        always {
            echo "This will always run regardless of the completion status"
            junit allowEmptyResults: true, testResults: "build/reports/**/*.xml"
        }
        cleanup {
            echo "Cleaning the workspace"
            cleanWs()
        }
        success {
            echo "This will run if the build succeeded"
        }
        failure {
            echo "This will run if the job failed"
        }
        unstable {
            echo "This will run if the completion status was 'unstable', usually by test failures"
        }
        changed {
            echo "This will run if the state of the pipeline has changed"
            echo "For example, if the previous run failed but is now successful"
        }
        fixed {
            echo "This will run if the previous run failed or unstable and now is successful"
        }
    }
}
