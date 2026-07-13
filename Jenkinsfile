pipeline {

    agent any

    stages {

        stage('Checkout') {

            steps {

                git branch: 'master',
                url: 'https://github.com/nageshjdevops/ansible-war.git'

            }
        }


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
                -i ansible/inventory \
                ansible/deploy-war.yml

                '''

            }
        }


        stage('Verify Deployment') {

            steps {

                sh '''

                curl http://172.31.11.148:8080/sample-app

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
