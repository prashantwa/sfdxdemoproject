#!groovy
import groovy.json.JsonSlurperClassic
node {

    def BUILD_NUMBER=env.BUILD_NUMBER
    def RUN_ARTIFACT_DIR="tests/${BUILD_NUMBER}"
    def SFDC_USERNAME

    def HUB_ORG= env.HUB_ORG_DH
    def SFDC_HOST = env.SFDC_HOST_DH
    def JWT_KEY_CRED_ID = env.JWT_CRED_ID_DH
    def CONNECTED_APP_CONSUMER_KEY= env.CONNECTED_APP_CONSUMER_KEY_DH
	
    def toolbelt = tool 'toolbelt'

    stage('checkout source') {
        // when running in multi-branch job, one must issue this command
        checkout scm
    }
	stage('Authorize'){
		rc = sh returnStatus: true, script: "${toolbelt}/sfdx _ force:auth:jwt:grant --clientid ${CONNECTED_APP_CONSUMER_KEY} --username ${HUB_ORG} --jwtkeyfile C:\'\\'Users\'\\'p.rameshwar.wayal\'\\'SFDXKeys\'\\'server.key --setdefaultdevhubusername --instanceurl ${SFDC_HOST}"
        if (rc != 0) { error 'hub org authorization failed' }
	}
	/*
    withCredentials([file(credentialsId: JWT_KEY_CRED_ID, variable: 'jwt_key_file')]) {
        stage('Authorize') {
            //rc = sh returnStatus: true, script: "${toolbelt}/sfdx _ force:auth --help"
            //echo '*** demo *** '
            rc = sh returnStatus: true, script: "${toolbelt}/sfdx _ force:auth:jwt:grant --clientid ${CONNECTED_APP_CONSUMER_KEY} --username ${HUB_ORG} --jwtkeyfile C:\'\\'Users\'\\'p.rameshwar.wayal\'\\'Jenkins\'\\'workspace\'\\'dx_pipeline_develop-SZ2UJ7X7IQNW7VEWRL6I6NUAYZ3Z3SR5RCEVNQDIODB7QHVK7GNA@tmp\'\\'secretFiles\'\\'28c95da4-84fd-4dbb-bc9c-ebe3a37c817d\'\\'server.key --setdefaultdevhubusername --instanceurl ${SFDC_HOST}"
            if (rc != 0) { error 'hub org authorization failed' }
            
        }

    }*/

}
