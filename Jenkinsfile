pipeline {
    agent any

    stages {
        stage('Clone') {
            steps {
                echo "Repository cloned from SCM"
            }
        }

        stage('List Files') {
            steps {
                sh "ls -la"
            }
        }

        stage('Sleep') {
            steps {
                sh "sleep 5"
            }
        }

        stage('Run') {
            steps {
                sh "echo 'Pipeline run completed'"
            }
        }
    }
}
