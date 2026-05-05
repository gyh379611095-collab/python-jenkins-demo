pipeline {
    agent any

    stages {
        stage('拉取代码') {
            steps {
                echo '正在拉取代码...'
                checkout scm
            }
        }
        stage('安装依赖') {
            steps {
                sh '''
                    apt-get install -y python3-pip
                    pip3 install pytest --break-system-packages
                '''
            }
        }
        stage('运行测试') {
            steps {
                sh 'pytest test_calculator.py -v'
            }
        }
    }

    post {
        success {
            echo '✅ 所有测试通过！'
        }
        failure {
            echo '❌ 测试失败，请检查代码！'
        }
    }
}