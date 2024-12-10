node {
    
    stage('Clone Repo') {
        git branch: 'main', url: 'https://github.com/SafaSALHA/examen-devops.git'
    }

    stage('Build Project') {
        sh "mvn clean package"
    }

    stage('Build Docker Image') {
        sh "docker build -t safa318/salutation:v1.0 ."
    }

    stage('Push Docker Image') {
        withCredentials([usernamePassword(credentialsId: 'docker-hub-credentials', 
                                          usernameVariable: 'DOCKER_USERNAME', 
                                          passwordVariable: 'DOCKER_PASSWORD')]) {
            sh '''
                echo $DOCKER_PASSWORD | docker login -u $DOCKER_USERNAME --password-stdin
                docker push safa318/salutation:v1.0
                docker logout
            '''
        }
    }

   
}
