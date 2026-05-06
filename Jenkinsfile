pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Test') {
            steps {
                echo "Running tests on branch: ${env.BRANCH_NAME}"
                sh 'pip install -r requirements.txt --break-system-packages'
                sh 'pytest test_calculator.py'
            }
        }

        // 只有在 main 分支才执行的“生产部署”
        stage('Deploy to Prod') {
            when {
                branch 'main'
            }
            steps {
                echo 'Deploying to PRODUCTION environment...'
                sh 'mkdir -p /tmp/prod_deploy && cp -r . /tmp/prod_deploy/'
            }
        }

        // 只有在 dev 分支才执行的“测试环境部署”
        stage('Deploy to Dev/QA') {
            when {
                branch 'dev'
            }
            steps {
                echo 'Deploying to DEV/QA environment...'
                sh 'mkdir -p /tmp/dev_deploy && cp -r . /tmp/dev_deploy/'
            }
        }
    }
}