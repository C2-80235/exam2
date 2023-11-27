pipeline {
    agent any

    stages {
        stage ('Pull image from github') {
            steps {
                git branch: 'main', url: 'https://github.com/C2-80235/devops-nov-27.git'
            }
        }
        stage ('build image') {
              steps {
                  sh '/usr/bin/docker image build -t shnk/exam-image .'
              }
          }
        stage ('login to docker hub') {
            steps {
                sh 'echo dckr_pat_eB-g-nh0WP5R_EiJ7gKVISmne38 | /usr/bin/docker login -u shnk --password-stdin'
            }
        }
        stage ('push image to docker hub') {
            steps {
                sh '/usr/bin/docker image push shnk/exam-image'
            }
        }
        stage ('delete docker service') {
            steps {
                sh '/usr/bin/docker service rm exam-service'
            }
        }
        stage ('start docker service') {
            steps {
                sh '/usr/bin/docker service create --name exam-service -p 9877:80 --replicas 5 shnk/exam-image'
            }
        }
    }
}
