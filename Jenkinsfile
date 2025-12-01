// Jenkinsfile - With Branch Selection Parameter

pipeline {
    agent any

    // Define parameters for the pipeline run.
    parameters {
        // A choice parameter to select which branch to clone.
        choice(name: 'BRANCH_TO_BUILD',
               choices: ['main', 'branch1', 'branch2'], // List all branches you want to make selectable
               description: 'Select the Git branch to clone and build')
    }

    stages {
        // Stage 1: Clone Selected Branch
        stage('1. Clone Selected Branch') {
            steps {
                echo "--- Stage 1: Cloning Git repository ---"
                echo "Cloning branch: ${params.BRANCH_TO_BUILD}"

                // Clean out the workspace before cloning to ensure a fresh start
                cleanWs()

                // Clone the repository using the selected branch parameter
                // 'scm' refers to the SCM configuration of the Jenkins job itself.
                // This is the most common way to clone the repo associated with the Jenkinsfile.
                checkout scm: [$class: 'GitSCM',
                              branches: [[name: 'refs/heads/${params.BRANCH_TO_BUILD}']],
                              userRemoteConfigs: [[url: 'https://github.com/MadhanVelpula/jenkinstest4']]]
                // IMPORTANT: Replace 'YOUR_GITHUB_USERNAME' and 'my-python-app.git' with your actual repo details.
                // If your repo is private, you might also need credentials:
                // credentialsId: 'YOUR_GITHUB_CREDENTIALS_ID_FROM_JENKINS'

                echo "Repository cloned successfully."
            }
        }

        // Stage 2: Verify app.py existence and content
        stage('2. Verify app.py') {
            steps {
                echo "--- Stage 2: Verifying app.py ---"
                sh 'ls -la app.py' // Confirm app.py exists in the workspace
                sh 'cat app.py'    // Display the content of app.py
            }
        }

        // Stage 3: Run app.py
        stage('3. Run Python App') {
            steps {
                echo "--- Stage 3: Running app.py ---"
                // Execute the python script. Ensure Python is installed on your Jenkins agent.
                sh 'python3 app.py' // Use 'python' or 'python3' depending on your system
            }
        }
    }

    post {
        always {
            echo "--- Post-build actions ---"
            echo 'Pipeline finished. Check console output for app.py results.'
        }
        success {
            echo 'Pipeline succeeded!'
        }
        failure {
            echo 'Pipeline failed! Review the logs for errors.'
        }
    }
}
