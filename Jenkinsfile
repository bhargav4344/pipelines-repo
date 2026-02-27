node('slave') {

    def startTime = System.currentTimeMillis()

    try {

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

        def endTime = System.currentTimeMillis()
        def duration = (endTime - startTime) / 1000

        echo "Scripted pipeline executed successfully in ${duration} seconds"

        emailext(
            subject: "SUCCESS: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
            body: """
Hello BHARGAV,

Your scripted Jenkins pipeline completed successfully.

Job Name   : ${env.JOB_NAME}
Build No   : ${env.BUILD_NUMBER}
Duration   : ${duration} seconds
Status     : SUCCESS

Build URL:
${env.BUILD_URL}

Regards,
Jenkins CI
""",
            to: "bhargavmapati04@gmail.com"
        )

    } catch (err) {

        def endTime = System.currentTimeMillis()
        def duration = (endTime - startTime) / 1000

        echo "Scripted pipeline failed after ${duration} seconds"

        emailext(
            subject: "FAILURE: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
            body: """
Hello Bhargav,

Your scripted Jenkins pipeline has FAILED.

Job Name   : ${env.JOB_NAME}
Build No   : ${env.BUILD_NUMBER}
Duration   : ${duration} seconds
Status     : FAILURE

Build URL:
${env.BUILD_URL}

Please check the console logs for details.

Regards,
Jenkins CI
""",
            to: "bhargavmapati04@gmail.com"
        )

        throw err
    }
}