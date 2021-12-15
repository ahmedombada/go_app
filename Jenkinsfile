pipeline {
    def app

    stage('Clone repository') {
        /* Cloning the Repository to our Workspace */

        checkout scm
    }

    stage('Test Application') {
        
        sh "go test"
        
    }

    stage('Build image') {
        /* This builds the actual image */

        app = docker.build("fromjenkins")
    }

    stage('Push image') {
        
        docker.withRegistry('https://registry.ombada.tech:5000', 'docker-registry') {
            app.push("${env.BUILD_NUMBER}")
            app.push("latest")
            } 
                echo "Trying to Push my own docker registry"
    }
}

