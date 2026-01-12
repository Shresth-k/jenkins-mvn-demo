pipeline {
    agent any

    parameters {
        choice(
            name: 'MVN_CMD',
            choices: [
                'clean',
                'clean compile',
                'clean test',
                'clean package',
                'clean install'
            ],
            description: 'Select Maven command'
        )
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/Shresth-k/jenkins-mvn-demo.git'
            }
        }

        stage('Build') {
            steps {
                echo "Running: mvn ${params.MVN_CMD}"
                sh "mvn ${params.MVN_CMD}"
            }
        }
    }

    post {
        success {
            echo "Build succeeded, sending email..."
            emailext(
                to: 'shresthshrink@gmail.com',
                subject: "✅ SUCCESS: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                body: """
Hi Shresth,

Your Jenkins pipeline build was SUCCESSFUL 🎉

Job: ${env.JOB_NAME}
Build Number: ${env.BUILD_NUMBER}
Maven Command: mvn ${params.MVN_CMD}

Build URL:
${env.BUILD_URL}

– Jenkins
"""
            )
        }

        failure {
            echo "Build failed, sending email..."
            emailext(
                to: 'shresthshrink@gmail.com',
                subject: "❌ FAILED: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                body: """
Hi Shresth,

Your Jenkins pipeline build FAILED ❌

Job: ${env.JOB_NAME}
Build Number: ${env.BUILD_NUMBER}
Maven Command: mvn ${params.MVN_CMD}

Build URL:
${env.BUILD_URL}

– Jenkins
"""
            )
        }
    }
}
