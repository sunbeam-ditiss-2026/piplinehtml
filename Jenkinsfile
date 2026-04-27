pipeline {
    agent any
environment{

    DOCKER_USERNAME="sunbeamditiss2026"
    DOCKER_IMAGENAME="newimage"
}
    stages {
        // stage('SCM') {
        //     steps {
        //         // get the latest changes from github repository
        //         git "https://github.com/sunbeam-ditiss-2026/piplinehtml.git"
        //     }
        // }

        stage('build docker image') {
            steps {
                sh 'docker image build -t ${DOCKER_USERNAME}/${DOCKER_IMAGENAME} .'
            }
        }

        stage('docker login') {
            steps {
                withCredentials([string(credentialsId: 'DOCKER_TOKEN', variable: 'DOCKER_TOKEN')]) {
 sh 'echo ${DOCKER_TOKEN} | docker login -u ${DOCKER_USERNAME} --password-stdin'
                    
                }
               
            }
        }

        stage('push docker image') {
            steps {
                sh 'docker image push ${DOCKER_USERNAME}/${DOCKER_IMAGENAME}'
            }
        }
            stage('reload the service') {
            steps {
                sh 'docker service update --force --image ${DOCKER_USERNAME}/${DOCKER_IMAGENAME} pipeline'
            }
        }
    }
}