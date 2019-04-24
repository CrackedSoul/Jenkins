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
						${ENV}
						
						(���ʼ��ǳ����Զ��·��ģ�����ظ���)<br/><hr/>
						
						��Ŀ���ƣ�${JOB_NAME}<br/><hr/>
						
						������ţ�${BUILD_NUMBER}<br/><hr/>

                """,
                to: "huangyulong@mastercom.cn",  
                recipientProviders: [[$class: 'DevelopersRecipientProvider']]
                )
    	}
    }
}