node {
    def app
    stage('Clone repository') {
        checkout scm
    }
    stage('Build image') {
       if(env.BRANCH_NAME == 'dev') {
       app = docker.build("dimitrijatimeski/kiii-jenkins")
       }
    }
    stage('Push image') {   
        if(env.BRANCH_NAME == 'dev') {
        docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
            app.push("${env.BRANCH_NAME}-${env.BUILD_NUMBER}")
            app.push("${env.BRANCH_NAME}-latest")
            // signal the orchestrator that there is a new version
            }
        }
        else {
            echo "Skipping Docker image push because the branch being built is not 'dev'."
        }
    }
}
