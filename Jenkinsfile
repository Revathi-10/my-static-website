pipeline {
    agent any

    environment {
        GITHUB_REPO = 'https://github.com/Revathi-10/my-static-website.git'
        GITHUB_BRANCH = 'gh-pages'
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Deploy') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'github-creds', usernameVariable: 'GIT_USER', passwordVariable: 'GIT_PASS')]) {
                    sh '''
                        git config user.name "${GIT_USER}"
                        git config user.email "you@example.com"

                        mkdir deploy
                        cp -r * deploy || true

                        git checkout --orphan ${GITHUB_BRANCH}
                        git rm -rf . || true
                        cp -r deploy/* . || true
                        rm -rf deploy

                        git add .
                        git commit -m "Deploy site"
                        git push -f https://${GIT_USER}:${GIT_PASS}@github.com/Revathi-10/my-static-website.git ${GITHUB_BRANCH}
                    '''
                }
            }
        }
    }
}
