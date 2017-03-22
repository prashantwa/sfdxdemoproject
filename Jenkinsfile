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

    stage('Create Scratch Org') {
        rc = sh returnStatus: true, script: "C:/Program Files/Heroku/bin/sfdx _ force:auth:jwt:grant -i 3MVG9YDQS5WtC11pWi_GyYnepWRkE5ksP1pQSaX.HxQtZbrwGGLuGJXiKfgFtlXsKTR4.eAubAB33.47sd9_p -r https://login.salesforce.com -f C:/Users/p.rameshwar.wayal/SFDXKeys/server.key -u dxpilot+p.rameshwar.wayal@accenture.com --setdefaultdevhubusername"
        if (rc != 0) { error 'hub org authorization failed' }
        else{ echo '*** rc *** '+rc }

    }

}
