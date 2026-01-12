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
}
