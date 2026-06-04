pipeline {


agent {
    label 'mangalam'
}

stages {

    stage('Build Docker Image') {
        steps {
            bat 'docker build -t abhinav654/shopease:latest .'
        }
    }

    stage('Docker Login') {
        steps {
            withCredentials([
                usernamePassword(
                    credentialsId: 'dockerhub',
                    usernameVariable: 'DOCKER_USER',
                    passwordVariable: 'DOCKER_PASS'
                )
            ]) {
                bat 'docker login -u %DOCKER_USER% -p %DOCKER_PASS%'
            }
        }
    }

    stage('Push Docker Image') {
        steps {
            bat 'docker push abhinav654/shopease:latest'
        }
    }
}

post {
    success {
        echo 'Docker Image Pushed Successfully'
    }

    failure {
        echo 'Build Failed'
    }
}


}
