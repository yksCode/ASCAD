pipeline {
    agent any

    environment {
        GRADLE_USER_HOME = "${WORKSPACE}/.gradle"
    }

    triggers {
        githubPush() // GitHub webhook 自动触发
    }

    stages {
        stage('Checkout') {
            steps {
                echo "==== 拉取代码 ===="
                git branch: 'main', url: 'https://github.com/yourname/your-repo.git', credentialsId: 'github-token'
            }
        }

        stage('Build') {
            steps {
                echo "==== 构建项目 ===="
                sh 'gradle clean build -x test'
            }
        }
        stage('Test') {
            steps {
                sh 'gradle test'
            }
        }

        stage('Package') {
            steps {
                echo "==== 打包 ===="
                sh './gradlew assemble'
                archiveArtifacts artifacts: 'build/libs/*.jar', fingerprint: true
            }
        }

        stage('Deploy') {
            steps {
                echo "==== 模拟部署 ===="
                sh 'echo "部署完成 ✅"'
            }
        }
    }

    post {
        success {
            echo "✅ 构建成功！"
        }
        failure {
            echo "❌ 构建失败，请查看日志！"
        }
    }
}
