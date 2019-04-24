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
                subject: "${PROJECT_NAME} - Build # ${BUILD_NUMBER} - ${BUILD_STATUS}!",
                body: """
		                ${PROJECT_NAME} - Build # ${BUILD_NUMBER} - ${BUILD_STATUS}:

						Check console output at $BUILD_URL to view the results.
						<hr/>
						
						(���ʼ��ǳ����Զ��·��ģ�����ظ���)<br/><hr/>
						
						��Ŀ���ƣ�${PROJECT_NAME}<br/><hr/>
						
						������ţ�${BUILD_NUMBER}<br/><hr/>
						
						svn�汾�ţ�${SVN_REVISION}<br/><hr/>
						
						����״̬��${BUILD_STATUS}<br/><hr/>
						
						����ԭ��${CAUSE}<br/><hr/>
						
						������־��ַ��<a href=\"${BUILD_URL}console\">${BUILD_URL}console</a><br/><hr/>
						
						������ַ��<a href=\"${BUILDURL}\">${BUILD_URL}</a><br/><hr/>

                """,
                to: "huangyulong@mastercom.cn",  
                recipientProviders: [[$class: 'DevelopersRecipientProvider']]
                )
    	}
    }
}