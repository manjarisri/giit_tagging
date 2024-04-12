pipeline {
    agent any

    environment {
        GIT_URL = 'https://github.com/manjarisri/giit_tagging.git'
        GIT_USERNAME = 'manjarisri'
        GIT_PASSWORD = '#Nanami0307'
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

         stage('Handle Webhook') {
            steps {
                script {
                    // Extract event type and branch from the GitHub payload
                    def eventType = env.CHANGE_EVENT
                    def branch = env.CHANGE_BRANCH

                    if (eventType == 'pull_request' && branch == 'main') {
                        echo "Webhook received for a merge into the main branch. Proceeding with tag generation."

                        // Generate and push tag
                        echo "Generating and pushing tag for branch: ${branch}"
                        def tagName = "${branch.toUpperCase()}-0.0.${env.BUILD_NUMBER}"
                        sh "git tag -a ${tagName} -m 'Auto-generated tag ${tagName}'"
                        withCredentials([usernamePassword(credentialsId: env.GIT_CREDENTIALS, usernameVariable: 'git_username', passwordVariable: 'git_password')]) {
                            def repoUrl = "${env.GIT_URL}".replace("https://", "")
                            sh "git push https://${GIT_USERNAME}:${GIT_PASSWORD}@${repoUrl} --tags"
                        }
                    } else {
                        echo "Webhook received, but not for a merge into the main branch. Skipping tag generation."
                    }
                
         
                }
            }
    }  
}

}
