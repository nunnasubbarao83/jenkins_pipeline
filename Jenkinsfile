pipeline {
  environment {
    registry = "22249292/first"
    registryCredential = 'dockerhub'
    dockerImage = ''
  }
 agent any
stages {
stage('Cloning our Git') {
steps {
git 'https://github.com/nunnasubbarao83/jenkins_pipeline.git'
}
}
stage('Building our image') {
steps{
script {
dockerImage = docker.build registry + ":$BUILD_NUMBER"
}
}
}
stage('Deploy our image') {
steps{
script {
docker.withRegistry( '', registryCredential ) {
dockerImage.push()
}
}
}
}
stage('Cleaning up') {
steps{
sh "docker rmi $registry:$BUILD_NUMBER"
}
}
}
}
