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
                sh 'mvn vdadsda'
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
                subject: "'${JOB_NAME} [${BUILD_NUMBER}]' ��������",
                body: """
		                ���飺
		                SUCCESSFUL: Job '${JOB_NAME} [${BUILD_NUMBER}]'
		                ״̬��${JOB_NAME} jenkins ������������ 
		                URL ��${BUILD_URL}
		                ��Ŀ���� ��${JOB_NAME} 
		                ��Ŀ���½��ȣ�${BUILD_NUMBER}
                """,
                to: "huangyulong@mastercom.cn",  
                recipientProviders: [[$class: 'DevelopersRecipientProvider']]
                )
    	}
    }
}