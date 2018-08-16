pipeline {
    agent {
            label "ansible1"
        }
        environment {
            DIR = "/home/ansible/"
        }
    stages {
        stage('clone') {
            steps {
                sh 'rm -rf ${DIR}docker; cd $DIR; git clone http://gitlab.example.com/skynet/docker.git'
            }
        }
        stage('pull_image') {
            steps {
              sh 'ansible-playbook ${DIR}docker/pull_image.yml'
            }
        }
        stage('create custom images') {
            steps {
              sh 'ansible-playbook ${DIR}docker/create_image.yml'
            }
        }
        stage('create container'){
          steps{
              sh 'ansible-playbook ${DIR}docker/create_container.yml'
          }
        }
        stage('validate container'){
          steps{
              sh 'ansible-playbook ${DIR}docker/dockerhost_validator.yml'
          }
        }
    }
}
