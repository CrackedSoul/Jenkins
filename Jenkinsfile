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
                sh 'docker images'
            }
        }
    }
    post{
    	always {
    	emailext (
                subject: "${JOB_NAME} - Build # ${BUILD_NUMBER} - ",
                body: """
		                ${JOB_NAME} - Build # ${BUILD_NUMBER} - :

						Check console output at $BUILD_URL to view the results.
						<hr/>
						
						(本邮件是程序自动下发的，请勿回复！)<br/><hr/>
						
						项目名称：${JOB_NAME}<br/><hr/>
						
						构建编号：${BUILD_NUMBER}<br/><hr/>
						
						svn版本号：${SVN_REVISION}<br/><hr/>
						
						触发原因：${CAUSE}<br/><hr/>
						
						构建日志地址：<a href=\"${BUILD_URL}console\">${BUILD_URL}console</a><br/><hr/>
						
						构建地址：<a href=\"${BUILDURL}\">${BUILD_URL}</a><br/><hr/>

                """,
                to: "huangyulong@mastercom.cn",  
                recipientProviders: [[$class: 'DevelopersRecipientProvider']]
                )
    	}
    }
}