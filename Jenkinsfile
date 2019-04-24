pipeline {
    agent any
    stages {
        stage('Stage1') {
            agent {
                    docker {
                        image 'maven:3-alpine'
                        args '-v /root/.m2:/root/.m2 -v /root/.m2/settings.xml:/usr/share/maven/conf/settings.xml'
                    }
            }
            steps {
                echo 'Hello Maven..'
                sh 'mvn -v'
            }
        } 
        stage('Stage2') {           
            steps {
                echo 'Hello, Stage2.'
            }
        }
    }
    post{
    	success {
    	emailext (
                subject: "'${JOB_NAME} [${BUILD_NUMBER}]' 更新正常",
                body: """
                详情：
                SUCCESSFUL: Job '${JOB_NAME} [${BUILD_NUMBER}]'
                状态：${JOB_NAME} jenkins 更新运行正常 
                URL ：${BUILD_URL}
                项目名称 ：${JOB_NAME} 
                项目更新进度：${BUILD_NUMBER}
                """,
                to: "huangyulong@mastercom.cn",  
                recipientProviders: [[$class: 'DevelopersRecipientProvider']]
                )
    	}
    }
}