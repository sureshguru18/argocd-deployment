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
                        sh "cat Chart.yaml"
			sh "sed -i 's+appVersion: .*\$+appVersion: \"${DOCKERTAG}\"+g' Chart.yaml"
			//sh "sed -i 's+appVersion: .*\$+appVersion: \"\${DOCKERTAG}\"+g' Chart.yaml"
			sh "cat Chart.yaml"
                        sh "git add ."
                        sh "git commit -m 'Done by Jenkins Job changemanifest: ${env.BUILD_NUMBER}'"
                        sh "git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/${GIT_USERNAME}/argocd-deployment.git HEAD:main"
      }
    }
  }
}
}
