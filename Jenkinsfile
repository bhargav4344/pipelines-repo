node('slave') {

    def mvnHome = tool 'maven3'

    stage('Checkout') {
        echo 'Checking out source code'
        git branch: 'main',
            credentialsId: 'b264fd28-449f-4b2b-a097-755314dc3d98',
            url: 'https://github.com/bhargav4344/pipelines-repo.git'
    }

    stage('Build') {
        echo 'Running Maven build'
        sh "${mvnHome}/bin/mvn clean compile"
    }

    stage('Test') {
        echo 'Running Maven tests'
        sh "${mvnHome}/bin/mvn test"
    }

    stage('Package') {
        echo 'Packaging artifact'
        sh "${mvnHome}/bin/mvn package"
    }

    stage('Archive') {
        archiveArtifacts artifacts: '**/target/*.jar', fingerprint: true
    }
}