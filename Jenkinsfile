 pipeline {
  agent any
    stages {
        stage('Pull') {
             steps{
                script{
                    checkout([$class: 'GitSCM', branches: [[name: '*/master']],
                        userRemoteConfigs: [[ 
                        	credentialsId: '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',
                            	url: 'https://github.com/mannai-web/MyApp.git']]])
                }
            }
        }
 stage('npm-Install') {
             steps{
                script{
                    sh "sudo npm install"
                }
            }
        }
stage('build') {
steps{

script {

sh "ansible-playbook Ansible/build.yml -i Ansible/inventory/host.yml "

}
}
} 

        stage('docker')
{
                  steps {
                         script{
                         sh "ansible-playbook Ansible/docker.yml -i Ansible/inventory/host.yml "
                                }
                        }
  }
stage('docker_registry') {
steps{
script {


sh "ansible-playbook Ansible/docker-registry.yml -i Ansible/inventory/host.yml "


}
}
}
}
}
