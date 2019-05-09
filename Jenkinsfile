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
        stage("FtpUpload"){
        	steps{
        		ftpPublisher alwaysPublishFromMaster: true, continueOnError: false, failOnError: false, publishers: [[configName: 'FtpTest', transfers: [[asciiMode: false, cleanRemote: false, excludes: '', flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: '', remoteDirectorySDF: false, removePrefix: '', sourceFiles: 'source.txt']], usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: false]]}
        }
    }
    post{
    	failure {
    	emailext (
    		body: """
    				${JOB_NAME}- Build #${BUILD_NUMBER} ${env.BUILD_STATUS}!</br>
	    			BUILD_URL: <a href=\"${env.BUILD_URL}\">${env.BUILD_URL}</a></br>
	    			JOB_URL:<a href=\"$JOB_URL\">$JOB_URL</a></br>
	    			CONSOLE:<a href=\"${env.BUILD_URL}console\">${env.BUILD_URL}console</br>
    		""", 
    		recipientProviders: [[$class: 'DevelopersRecipientProvider']], 
    		subject: '${JOB_NAME}- Build #${BUILD_NUMBER} Construction Result',   
    		to: 'huangyulong@mastercom.cn'
			)
		}
    }
}