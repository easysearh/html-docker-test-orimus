
pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                echo 'Building the application...'
                // Example build command
                sh 'docker build --no-cache -t jenkinsimage  .'
            }
        }
        stage('push') {
            steps {
                echo 'Running push...'
                sh 'docker tag jenkinsimage toxicmoel/jenkinsimage:${BUILD_ID}'
                sh 'docker login -u="toxicmoel" -p="Jesuisroot123@"'
                sh 'docker push toxicmoel/jenkinsimage:${BUILD_ID} '
                
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying the application...'
                
                sh 'ssh -o StrictHostKeyChecking=no -i "../my-first.pem" ec2-user@ec2-35-182-61-252.ca-central-1.compute.amazonaws.com -t "docker ps -aq | xargs docker rm -f; docker run -p 80:80 -d toxicmoel/jenkinsimage:${BUILD_ID}"'
                
            }
        }
    }
}
