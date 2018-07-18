def notifySlack(String buildStatus = 'STARTED') {
    // Build status of null means success.
    buildStatus = buildStatus ?: 'SUCCESS'
    
    def msg = "${buildStatus}: `${env.JOB_NAME}` #${env.BUILD_NUMBER}:-Docker images are pulled and deployed into Docker Swarm by shrilekha.s"

    slackSend(message: msg)
}

node {
    checkout scm
    stage('build') {
        /* Create docker swarm */
         sh "ansible-playbook -i /etc/ansible/inventory/hosts /etc/ansible/playbooks/eia-deploy-microservice.yml"           
    }
    try {      
        notifySlack(currentBuild.result)
        // Existing build steps.
    } catch (e) {
        currentBuild.result = 'FAILURE'
        throw e
    } 
}
