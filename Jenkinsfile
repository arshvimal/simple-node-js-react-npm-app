pipeline {
    agent {
        docker {
            image 'node:18'
            args '-u root:root'
        }
    }
    stages {
        stage('Install SSH') {
            steps {
                sh 'apt-get update && apt-get install -y openssh-client rsync'
            }
        }
        stage('Deploy') {
            steps {
                sshagent(['node2-ssh-key']) {
                    sh '''
                    ssh -o StrictHostKeyChecking=no arshvml@34.131.121.197 'echo Connected!'
                    rsync -avz --delete ./ arshvml@34.131.121.197:/home/arshvml/simple-node-js-react-npm-app/
                    '''
                }
            }
        }
    }
}