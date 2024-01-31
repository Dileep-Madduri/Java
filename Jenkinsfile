pipeline {
    agent any

    tools {nodejs "nodejs"}
    environment {
        CHECKLY_API_KEY = credentials('checkly-api-key')
        CHECKLY_ACCOUNT_ID = credentials('checkly-account-id')
        CHECKLY_TEST_ENVIRONMENT='production'
    }

    stages {
        stage('Deploy') {
            steps {
                echo 'Deploying....'
            }
        }
        stage('Dependencies') {
            steps {
                sh 'npm ci'
            }
        }
        stage('checkly test') {
            steps {
                sh 'npx checkly test --record'
            }
        }
        stage('checkly deploy') {
            when {
                branch "main"
            }
            steps {
                sh 'npx checkly deploy --force'
            }
        }
    }
}
