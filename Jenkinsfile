node {
    def app
    
    stage('Clone repository') {

        checkout scm
    }
    stage('Update GIT') {
        script {
                catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                    withCredentials([usernamePassword(credentialsId: 'github-auth-token', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
                        sh "git config user.email scott.sorell@gmail.com"
                        sh "git config user.name whentimeslows"
                        sh "cat vote-ui-deployment.yaml"
                        sh "sed -i 's+whentimeslows/vote.*+whentimeslows/vote:${DOCKERTAG}+g' vote-ui-deployment.yaml"
                        sh "cat vote-ui-deployment.yaml"
                        sh "git add ."
                        sh "git commit -m 'Done by Jenkins Job deployment: ${env.BUILD_NUMBER}'"
                        sh "git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/${GIT_USERNAME}/vote-deploy.git HEAD:master"
                    }
                }
            }
    }
}
