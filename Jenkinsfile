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
		              ${BUILD_NUMBER}
		              ${JOB_NAME}
		              ${CHANGES} 

                """,
                to: "huangyulong@mastercom.cn",  
                recipientProviders: [[$class: 'DevelopersRecipientProvider']]
                )
    	}
    }
}