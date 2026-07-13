pipeline {

    agent any

    tools {
        maven 'maven3'
    }

    stages {

        stage('Build WAR') {
            steps {
                sh '''
                mvn clean package
                '''
            }
        }

        stage('Deploy WAR') {
            steps {
                sh '''
                export ANSIBLE_HOST_KEY_CHECKING=False

                ansible-playbook \
                  -i inventory \
                  ansible-war.yaml
                '''
            }
        }

        stage('Verify Deployment') {
            steps {
                sh '''
                curl -f http://172.31.11.148:8080/LoginWebApp
                '''
            }
        }

    }

    post {

        success {
            echo "Deployment Successful"
        }

        failure {
            echo "Deployment Failed"
        }

    }

}
