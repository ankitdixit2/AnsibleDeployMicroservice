node {
    checkout scm
    stage('build') {
        /* Create docker swarm */
         sh "sudo ansible-playbook -i /etc/ansible/inventory/hosts /etc/ansible/playbooks/eia-deploy-microservice.yml"           
    }
}
