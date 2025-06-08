pipeline {
    agent any

    environment {
        GITHUB_REPO = 'https://github.com/Revathi-10/my-static-website.git'
        GITHUB_USERNAME = 'Revathi-10'
        GITHUB_EMAIL = 'revathims.22cse@cambridge.edu.in'
        GITHUB_BRANCH = 'gh-pages'
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build Site') {
            steps {
                echo 'No build needed for static HTML site.'
            }
        }

        stage('Deploy to GitHub Pages') {
            steps {
                withCredentials([string(credentialsId: 'github-pat', variable: 'GITHUB_TOKEN')]) {
                    sh '''
                        git config user.name "${GITHUB_USERNAME}"
                        git config user.email "${GITHUB_EMAIL}"

                        # Create temporary deployment folder
                        mkdir deploy
                        cp -r * deploy || true

                        # Switch to gh-pages branch
                        git checkout --orphan ${GITHUB_BRANCH}
                        git rm -rf . || true
                        cp -r deploy/* . || true
                        rm -rf deploy

                        git add .
                        git commit -m "Deploy static site to GitHub Pages"
                        git push -f https://${GITHUB_TOKEN}@github.com/${GITHUB_USERNAME}/my-static-website.git ${GITHUB_BRANCH}
                    '''
                }
            }
        }
    }
}
