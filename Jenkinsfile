pipeline {
    agent any

    tools {nodejs "NODE18"}
    environment {
        CHECKLY_API_KEY = credentials('cu_27dad56d5ac5434e85f0686e02628712')
        CHECKLY_ACCOUNT_ID = credentials(' 1e3c47f2-28a0-455c-a2f8-ff209589821e')
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
