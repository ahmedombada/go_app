
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
// node {
//     def app

//     stage('Clone repository') {
//         /* Cloning the Repository to our Workspace */

//         checkout scm
//     }

//     stage('Test App') {
        
//         sh "go test"
        
//     }
    
//     stage('Build image') {
//         /* This builds the actual image */

//         app = docker.build("fromjenkins")
//     }

//     stage('Push image') {
        
//         docker.withRegistry('https://registry.ombada.tech:5000', 'docker-registry') {
//             app.push("${env.BUILD_NUMBER}")
//             app.push("latest")
//             } 
//                 echo "Trying to Push my own docker registry"
//     }
// }

// with ansible

node {
    def app


    stage('Test App') {
        
        sh '''
          ansible --version
          ansible-playbook --version
          ansible-galaxy --version
        '''        
    }
    
    
}