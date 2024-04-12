pipeline {
    agent any

    environment {
        GIT_URL = 'https://github.com/manjarisri/giit_tagging.git'
        GIT_CREDENTIALS = 'github'
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                // Replace this with your build commands
                sh 'echo "Building..."'
            }
        }

        stage('Test') {
            steps {
                // Replace this with your test commands
                sh 'echo "Testing..."'
            }
        }

         stage('Tag') {
            steps {
                echo "Generating and pushing tag for branch: ${env.BRANCH_NAME}"
                script {
                    // Set Git user
                    sh 'git config --global user.email "your-email@example.com"'
                    sh 'git config --global user.name "Your Name"'

                    // Generate tag name
                    def tagName = "${env.BRANCH_NAME.toUpperCase()}-0.0.${env.BUILD_NUMBER}"

                    // Tag the commit
                    sh "git tag -a ${tagName} -m 'Auto-generated tag ${tagName}'"

                    // Push the tag to the remote repository
                    withCredentials([usernamePassword(credentialsId: env.GIT_CREDENTIALS, usernameVariable: 'git_username', passwordVariable: 'git_password')]) {
                        // Extract the repository URL
                        def repoUrl = "${env.GIT_URL}".replace("https://", "")
                        sh "git push https://${git_username}:${git_password}@${repoUrl} --tags"
                    }
                }
            }
        }
    }
}
