pipeline {
    agent {
        label "ansiblenode"
    }

    stages {
        stage('Pull the Dockerfile From Github') {
            steps {
                git branch: 'main', url: 'https://github.com/Swaroop-751/Jenkinsfile_Dockerfile.git'
            }
        }

	stage('Build Docker Image') {
            steps {
                sh 'cd /home/ec2-user/jenkinsws/workspace/cloudproject && sudo docker build -t $JOB_NAME:v1.$BUILD_ID .'
		sh 'sudo docker images'
		sh 'sudo docker rmi $JOB_NAME:v1.$BUILD_ID'
            }
        }

	stage('Associate the Image name with Docker Hub ID') {
            steps{
                sh 'sudo docker image tag $JOB_NAME:v1.8 swar2001/$JOB_NAME:v1.8'
                sh 'sudo docker image tag $JOB_NAME:v1.8 swar2001/$JOB_NAME:latest'
            }
        }
    }
}