pipeline {
    agent any

    parameters {
        choice(
            name: 'BRANCH_TO_BUILD',
            choices: ['main', 'branch1', 'branch2'],
            description: 'Select the Git branch to clone and build'
        )
    }

    stages {

        stage('1. Clone Selected Branch') {
            steps {
                echo "--- Stage 1: Cloning Git repository ---"
                echo "Cloning branch: ${params.BRANCH_TO_BUILD}"

                cleanWs()

                checkout([
                    $class: 'GitSCM',
                    branches: [[name: "refs/heads/${params.BRANCH_TO_BUILD}"]],
                    userRemoteConfigs: [[
                        url: 'https://github.com/MadhanVelpula/jenkinstest4'
                        // If private repo → add: credentialsId: 'github-token'
                    ]]
                ])

                echo "Repository cloned successfully."
            }
        }

        stage('2. Verify app.py') {
            steps {
                echo "--- Stage 2: Verifying app.py ---"
                sh 'ls -la app.py'
                sh 'cat app.py'
            }
        }

        stage('3. Run Python App') {
            steps {
                echo "--- Stage 3: Running app.py ---"
                sh 'python3 app.py'
            }
        }
    }

    post {
        always {
            echo "--- Post-build actions ---"
            echo "Pipeline finished. Check console output."
        }
        success {
            echo "Pipeline succeeded!"
        }
        failure {
            echo "Pipeline failed! Review the logs."
        }
    }
}
