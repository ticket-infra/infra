
node{
    def app

     stage('Clone repository') {
         checkout scm
     }

     stage('Update Manifest'){
         script {
             withCredentials([usernamePassword(credentialsId: 'github', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]){
               sh "git config --global user.email 75758585@naver.com"
               sh "git config --global user.name leejunsu249"
               sh "sed -i 's/${BUILDNAME}:.*\$/node-gen:${DOCKERTAG}/g' k8s/${BUILDNAME}-depl.yaml"
               sh "git add k8s/${BUILDNAME}-depl.yaml"
               sh "git commit -m '[UPDATE] ${BUILDNAME}-depl ${DOCKERTAG} image versioning'"
               sh "git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/ticket-infra/infra.git HEAD:master"
            }

         }
     }
}