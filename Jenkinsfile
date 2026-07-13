pipeline {
    agent any

    environment {
        EC2_IP = "3.231.154.6"
    }

    stages {

        stage('Deploy to EC2') {
            steps {

                sshagent(credentials: ['ec2-ssh']) {

                    sh """
                    scp -r -o StrictHostKeyChecking=no * ubuntu@${EC2_IP}:/tmp/website/

                    ssh -o StrictHostKeyChecking=no ubuntu@${EC2_IP} '
                        sudo apt update
                        sudo apt install -y nginx

                        sudo mkdir -p /var/www/html
                        sudo rm -rf /var/www/html/*

                        sudo cp -r /tmp/website/* /var/www/html/

                        sudo systemctl restart nginx
                    '
                    """
                }

            }
        }

    }
}
