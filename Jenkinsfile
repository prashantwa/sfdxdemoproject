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

    withCredentials([file(credentialsId: JWT_KEY_CRED_ID, variable: 'jwt_key_file')]) {
        stage('Create Scratch Org') {
			//C:\'\\'Users\'\\'p.rameshwar.wayal\'\\'SFDXKeys\'\\'server.key
            rc = sh returnStatus: true, script: "\'${toolbelt}\'/"+"sfdx _ force:auth:jwt:grant --clientid ${CONNECTED_APP_CONSUMER_KEY} --username ${HUB_ORG} --jwtkeyfile C:\'\\'Users\'\\'p.rameshwar.wayal\'\\'SFDXKeys\'\\'server.key --setdefaultdevhubusername --instanceurl ${SFDC_HOST}"
            //rc = sh returnStatus:true, script: "\'${toolbelt}\'/"+"sfdx _ force:auth:web:login -i ${CONNECTED_APP_CONSUMER_KEY} -r ${SFDC_HOST} -d"
            def jsonSlurperObj = new JsonSlurperClassic()
            def aobj = jsonSlurperObj.parseText(rc)
            if (aobj.status != "ok") { error 'hub org authorization failed' }
            else{ echo '*** rc *** '+rc }
            
            //if (rc != 0) { error 'hub org authorization failed' }
            //else{ echo '*** rc *** '+rc }

            // need to pull out assigned username
            /*def rmsg = sh returnStdout: true, script: "\'${toolbelt}\'/"+"sfdx _ force:org:create --definitionfile config/workspace-scratch-def.json --json --setdefaultusername"
            println rmsg
            //echo '*** file content *** '+ rmsg
            def jsonSlurper = new JsonSlurperClassic()
            def robj = jsonSlurper.parseText(rmsg)
            if (robj.status != "ok") { error 'org creation failed: ' + robj.message }
            SFDC_USERNAME=robj.username
            echo '*** user Name *** '+SFDC_USERNAME
            robj = null
			*/
        }
		
    }
}
