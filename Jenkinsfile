pipeline {
    agent any
    tools {
        jdk 'jdk17'
        maven 'maven3'
    }
    stages {
        stage('1. 拉取代码') {
            steps {
              git url: 'https://github.com/augustusgao555/jenkins_test.git', branch: 'main'
            }
        }

        stage('2. 编译打包') {
            steps {
                dir('springboot-jenkins-demo') {
                    sh 'mvn clean package -DskipTests'
                }
            }
        }

        stage('3. 关闭旧服务') {
            steps {
                sleep 2
            }
        }

        stage('4. 启动 SpringBoot') {
            steps {
                dir('springboot-jenkins-demo') {
                    sh 'nohup java -jar target/*.jar > app.log 2>&1 &'
                    sleep 5
                    echo "✅ 启动成功！访问：http://虚拟机IP:8080/hello"
                }
            }
        }
    }
    post {
        success { echo "🎉 构建部署成功！" }
        failure { echo "❌ 构建失败！" }
    }
}
