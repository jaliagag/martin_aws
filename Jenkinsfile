pipeline {

    agent any

    stages {

        stage('Build') {
            steps {
                bitbucketStatusNotify(buildState: 'INPROGRESS')
                script {
                def REPO_NAME = scm.getUserRemoteConfigs()[0].getUrl().tokenize('/').last().split("\\.")[0]
                echo 'Using REMOTE Jenkinsfile from: ' + env.RJPP_SCM_URL + ' branch:  ' + env.RJPP_BRANCH
                echo 'Calling deploy-service for branch: ' + env.BRANCH_NAME
                if ((env.BRANCH_NAME == 'dev') || (env.BRANCH_NAME == 'rc')) {
                    build_service(REPO_NAME,env.BRANCH_NAME)
                } else if (env.BRANCH_NAME == 'master') {
                    build_service(REPO_NAME,'sandbox')
                    build_service(REPO_NAME,'demo')
                    build_service(REPO_NAME,'prod')
                }
                }
            }
        }
    }
}

def build_service(REPO_NAME,ENVIRONMENT) {
    try {
        build job: 'deploy-service-' + ENVIRONMENT, parameters: [string(name: 'enviroment', value: ENVIRONMENT) , string(name: 'service' , value: REPO_NAME)]
        bitbucketStatusNotify(buildState: 'SUCCESSFUL')  
    } catch (Exception e) {
            currentBuild.result = 'FAILED'
            bitbucketStatusNotify(buildState: 'FAILED')
            error("Failed")
        } 
}
