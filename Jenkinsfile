pipeline {
    agent any
    stages {
        stage('Stage1') {          
            steps {
                echo 'Hello Maven..'
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
        		checkout([$class: 'SubversionSCM', additionalCredentials: [], excludedCommitMessages: '', excludedRegions: '', excludedRevprop: '', excludedUsers: '', filterChangelog: false, ignoreDirPropChanges: false, includedRegions: '', locations: [[cancelProcessOnExternalsFail: true, credentialsId: 'f1c50f6f-4d25-4ab0-96b4-000afca668c0', depthOption: 'infinity', ignoreExternalsOption: true, local: './conf/', remote: 'https://svn.mastercom.cn:4438/svn/reopsitory/trunk/MTNOH_JAVAMTEX/配置中心文件/东莞网调']], quietOperation: true, workspaceUpdater: [$class: 'CheckoutUpdater']])
        		sh 'ls'
        		
        		ftpPublisher alwaysPublishFromMaster: false,masterNodeName:null, paramPublish:null,continueOnError: false, failOnError: false, publishers: [[configName: 'FtpTest', transfers: [[asciiMode: false, cleanRemote: false, excludes: '', flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: '', remoteDirectorySDF: false, removePrefix: '',sourceFiles: 'properties/**']], usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: false]]
        	}
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