node {
    def app

    stage('Clone repository') {
      

        checkout scm
    }

    stage('Update GIT') {
            script {
                catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                    withCredentials([usernamePassword(credentialsId: 'github', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
                        //def encodedPassword = URLEncoder.encode("$GIT_PASSWORD",'UTF-8')
                        sh "git config user.email sureshguru.kumar04@gmail.com"
                        sh "git config user.name Sureshguru18"
                        sh "cat values.yaml"
			sh "sed -i 's+tag: .*\$+tag: \"${DOCKERTAG}\"+g' values.yaml"
			//sh "sed -i 's+tag: .*\$+tag: \"\${DOCKERTAG}\"+g' values.yaml"
			sh "cat values.yaml"
                        sh "git add ."
                        sh "git commit -m 'Done by Jenkins Job changemanifest: ${env.BUILD_NUMBER}'"
                        sh "git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/${GIT_USERNAME}/argocd-deployment.git HEAD:main"
      }
    }
  }
}
}
