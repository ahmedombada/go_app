
// I dont think this is ideal
// node {
//     def app

//     stage('Clone repository') {
//         /* Cloning the Repository to our Workspace */

//         checkout scm
//     }

//     stage('Init App') {
        
//         sh "go mod init go-build"
        
//     }

//     stage('Init App') {
        
//         sh "go mod tidy"
        
//     }
    
//     stage('Test App') {
        
//         sh "go test"
        
//     }

//     stage('Build App') {
        
//         sh "go build app.go"
        
//     }
// }

// This is how you build a docker image and push it, here im using my own docker registery
node {
    def app
    cleanWs()
    
    stage('Stop ALL running containers') {
        sh "docker stop \$(docker ps -aq)"
    }

    stage('Clone repository') {
        /* Cloning the Repository to our Workspace */

        checkout scm
    }

    stage('Init App') {
        
        sh "go mod init go-build"
        
    }

    stage('Init App') {
        
        sh "go mod tidy"
        
    }

    stage('Test App') {
        
        sh "go test"
        
    }
    
    stage('Build image') {
        /* This builds the actual image */

        app = docker.build("test-jenkins-go")
    }

    stage('Push image') {
        
        docker.withRegistry('https://registry.ombada.tech:5000', 'docker-registry') {
            app.push("${env.BUILD_NUMBER}")
            app.push("latest")
            } 
                echo "Trying to Push my own docker registry"
    }

    stage('run image') {
        /* This runs image */

        sh "docker run -d -p 8088:8080 registry.ombada.tech:5000/test-jenkins-go"
    }

    stage('update image on remote server') {
        // This deploys the image to a second server // 
        ansiblePlaybook(credentialsId: 'svc-ssh', inventory: 'hosts', playbook: 'main.yml', disableHostKeyChecking: 'true')
    }
}

// with ansible

// node {
//     def app

//         stage('Clone repository') {
//         /* Cloning the Repository to our Workspace */

//         checkout scm
//     }


//     stage('Test App') {
        
//         sh '''
//           cd ansible-go/
//           echo 'test123' > .vault_pass
//           sudo ./run_playbook -t deploy-app --check

//         '''        
//     }
    
    
// }