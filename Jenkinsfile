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
                sh 'mvn fasfav'
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
    	failure {
    	emailext (
    		body: """
    			${JOB_NAME}- Build #${BUILD_NUMBER} Construction Result
    			BUILD_URL: ${env.BUILD_URL}
    			JOB_URL:$JOB_URL
    			LogInfo:${env.BUILD_URL}console
    		""", 
    		recipientProviders: [[$class: 'DevelopersRecipientProvider']], 
    		subject: '${JOB_NAME}- Build #${BUILD_NUMBER} Construction Result',   
    		to: 'huangyulong@mastercom.cn'
			)
		}
    }
}