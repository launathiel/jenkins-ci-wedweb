node {

    stage('Checkout') {
        checkout scm
    }

    stage('Configure ENV'){
        sh "chmod +x env.sh"
        sh "./env.sh"
        echo "env variable has been created!"
    }

    stage("Container Clean"){
        sh "docker-compose stop"
        sh "docker-compose rm -f"
    }

    stage('Image Build'){
        sh "docker-compose build"
        echo "Image build complete"
    }

    stage('Run App'){
        sh "docker-compose up -d"
        echo "Application started!"
    }

}
