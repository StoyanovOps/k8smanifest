pipeline { 
    agent { 
        node {
            label 'gradle-agent'
            }
    }
    stages {
        stage('Update GIT') {
                steps {
                    catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                        withCredentials([usernamePassword(credentialsId: 'github-argo', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
                            //def encodedPassword = URLEncoder.encode("$GIT_PASSWORD",'UTF-8')
                            //sh "git switch master"
                            sh "git config user.email stanislav.stoyanov@savvytribe.tech"
                            sh "git config user.name StoyanovOps"
                            sh "cat deployment.yaml"
                            sh "sed -i 's+stoyanovsavvy/savvytribe.*+stoyanovsavvy/savvytribe:${DOCKERTAG}+g' deployment.yaml"
                            sh "cat deployment.yaml"
                            sh "git add ."
                            sh "git commit -m 'Done by Jenkins Job changemanifest: ${env.BUILD_NUMBER}'"
                            sh "git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/${GIT_USERNAME}/k8smanifest.git HEAD:main"
                        } 
                    }
                }
            } 
        }   
    }