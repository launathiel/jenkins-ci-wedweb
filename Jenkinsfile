def CONTAINER_NAME="jenkins-pipeline"
def CONTAINER_TAG="latest"
def DOCKER_HUB_USER="launathiel"
def HTTP_PORT="80"

node {

    // stage('Initialize'){
    //     def dockerHome = tool 'myDocker'
    //     env.PATH = "${dockerHome}/bin:${env.PATH}"
    // }

    stage('Checkout') {
        checkout scm
    }

    stage('Configure ENV'){
        sh "chmod +x env.sh"
        sh "./env.sh"
        echo "env variable has been created!"
    }



    stage("Image Prune"){
        imagePrune()
    }

    stage('Image Build'){
        imageBuild()
    }

    // stage('Push to Docker Registry'){
    //     withCredentials([usernamePassword(credentialsId: 'dockerHubAccount', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
    //         pushToImage(CONTAINER_NAME, CONTAINER_TAG, USERNAME, PASSWORD)
    //     }
    // }

    stage('Run App'){
        runApp()
    }

}

def imagePrune(){
    try {
        sh "docker-compose stop"
        sh "docker-compose rm -f"
    } catch(error){}
}

def imageBuild(){
    // sh "docker build -t $containerName:$tag  -t $containerName --pull --no-cache ."
    sh "docker-compose build"
    echo "Image build complete"
}

// def pushToImage(containerName, tag, dockerUser, dockerPassword){
//     sh "docker login -u $dockerUser -p $dockerPassword"
//     sh "docker tag $containerName:$tag $dockerUser/$containerName:$tag"
//     sh "docker push $dockerUser/$containerName:$tag"
//     echo "Image push complete"
// }

def runApp(){
    sh "docker-compose up -d"
    echo "Application started!"
}