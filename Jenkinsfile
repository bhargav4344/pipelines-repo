node('slave') {

    def startTime = System.currentTimeMillis()
    def mvnHome = tool 'maven3'

    try {

        stage('Checkout') {
            git branch: 'main',
                credentialsId: 'b264fd28-449f-4b2b-a097-755314dc3d98',
                url: 'https://github.com/bhargav4344/pipelines-repo.git'
        }

        stage('Build') {
            sh "${mvnHome}/bin/mvn clean compile" 
        }

        stage('Test') {
            sh "${mvnHome}/bin/mvn test"
        }

        stage('Package') {
            sh "${mvnHome}/bin/mvn package"
        }

        stage('Archive') {
            archiveArtifacts artifacts: '**/target/*.jar', fingerprint: true
        }

        def endTime = System.currentTimeMillis()
        def duration = (endTime - startTime) / 1000

        echo "Scripted pipeline executed successfully in ${duration} seconds"
    }
}