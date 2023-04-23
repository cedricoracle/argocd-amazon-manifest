node {
    def app
    
    env.IMAGE = 'cedric96/amazon'

    stage('Clone repository') {
             git branch: 'main', url: 'https://github.com/cedricoracle/argocd-amazon-manifest.git'  
    }

    stage('Update GIT') {
            script {
                catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                    withCredentials([usernamePassword(credentialsId: 'cedric', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
                        //script {def encodedPassword = URLEncoder.encode("$GIT_PASSWORD",'UTF-8')}
                        //script  {def IMAGE='cedric96/amazon'}
                        sh "git config user.email wentitaju@gmail.com"
                        sh "git config user.name cedricoracle"
                        //sh "git switch master"
                        sh "cat deployment.yml"
                        sh "sed -i 's+${IMAGE}.*+${IMAGE}:${DOCKERTAG}+g' deployment.yml"
                        sh "cat deployment.yml"
                        sh "git add ."
                        sh "git commit -m 'Done by Jenkins Job changemanifest: ${env.BUILD_NUMBER}'"
                        sh "git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/${GIT_USERNAME}/argocd-manifest.git HEAD:main"
             }
         }
     }
  }
}
