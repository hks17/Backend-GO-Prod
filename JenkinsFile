node {
    // Parameters definition
    properties([
        parameters([
            string(name: 'DOCKERTAG', defaultValue: 'default_value', description: 'This is a parameter passed from another job')
            string(name: 'DOCKER_USERNAME', defaultValue: 'default_value', description: 'This is a parameter passed from another job')
            string(name: 'DOCKER_IMAGE', defaultValue: 'default_value', description: 'This is a parameter passed from another job')
        ])
    ])

    environment{
        GIT_CREDENTIALS_ID = 'hendri-backend-kou'
        GIT_REPO_URL = 'https://github.com/hks17/Backend-GO-Prod.git'
    }
    
    stage('Clone repository') {
      checkout scm
    }
    stage('Read Parameter') {
        echo "Received parameter: ${params.DOCKERTAG}"
    }
    
    stage('Update Git') {
        // steps {
            echo "Received parameter: ${params.DOCKERTAG}"
            withCredentials([gitUsernamePassword(credentialsId: 'helios-jenkins-new', gitToolName: 'Default')]) {
                sh "git config --global user.name hheelliiooss-admin"
                sh "git config --global user.email developerteamhelios@gmail.com"
                
                sh "cat deployment.yaml"
                sh "sed -i 's+${params.DOCKER_USERNAME}/${params.DOCKER_IMAGE}.*+${params.DOCKER_USERNAME}/${params.DOCKER_IMAGE}:${params.DOCKERTAG}+g' deployment.yaml"
                
                sh "cat deployment.yaml"
                sh "git add ."
                sh "git commit -m 'Done by Jenkins job update-deployment: ${params.DOCKERTAG}'"
                sh "git push ${environment.GIT_REPO_URL} HEAD:main"
                
            }
    }
}