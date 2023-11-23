pipeline {
    agent any

    stages {
        stage ('SCM') {
            steps {
                git branch: 'main', url: 'https://github.com/ovhatkar/jenkins.git'
            }
        }
        stage ('docker login') {
            steps {
                sh 'echo dckr_pat_3AGDVtcVbebHr2TxcAqRMM5f-KY | /usr/bin/docker login -u onkarvhatkar --password-stdin'
            }
        }
        stage ('docker build image') {
            steps {
                sh '/usr/bin/docker image build -t onkarvhatkar/mywebsite .'
            }
        }
        stage ('docker push image') {
            steps {
                sh '/usr/bin/docker image push onkarvhatkar/mywebsite'
            }
        }
        stage ('docker remove service') {
            steps {
                sh '/usr/bin/docker service rm myservice'
            }
        }
        stage ('docker create service') {
            steps {
                sh '/usr/bin/docker service create --name myservice -p 9090:80 --replicas 5 onkarvhatkar/mywebsite'
            }
        }
    }
}
