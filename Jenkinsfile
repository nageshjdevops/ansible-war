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
                ansible-playbook \
                  -i inventory \
                  ansible-war.yaml
                '''
            }
        }

        stage('Verify Deployment') {
            steps {
                sh '''
                curl -f http://172.31.11.148:8080/sample-app
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
