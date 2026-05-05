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
                    apt-get update -y
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
        stage('部署') {
            steps {
                echo '正在部署到生产目录...'
                sh '''
                    mkdir -p /var/jenkins_home/production
                    cp cal.py /var/jenkins_home/production/
                    cp test_calculator.py /var/jenkins_home/production/
                    echo "部署时间: $(date)" > /var/jenkins_home/production/deploy.log
                    echo "✅ 部署完成！"
                '''
            }
        }
    }

    post {
        success {
            echo '✅ 所有测试通过，部署成功！'
        }
        failure {
            echo '❌ 测试失败，不进行部署！'
        }
    }
}