pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: "${env.BRANCH_NAME}",
                    url: 'https://github.com/FirmansyahDzakwanArifien/learn-jenkins-multibranch_pipeline.git'
            }
        }

        stage('Build') {
            steps {
                echo "Building Docker image..."
                sh 'docker build -t learn-jenkins-multibranch .'
            }
        }

        stage('Test') {
            steps {
                echo "Running tests..."
                sh 'pip install flask pytest'
                sh 'pytest -v'
            }
        }
    }

    post {
        success {
            echo 'Build Sukses!'
            httpRequest(
                httpMode: 'POST',
                url: 'https://discord.com/api/webhooks/1425012152946790433/G0koVM0hfMK2tvsr48OO7sPH7m2OvtZmmP3_urPVq_Njj-eD7Dfxeia5aOP8WnxqxATN',
                requestBody: "{\"content\": \"✅ Build Sukses untuk branch ${env.BRANCH_NAME}\"}",
                contentType: 'APPLICATION_JSON'
            )
        }

        failure {
            echo 'Build Gagal!'
            httpRequest(
                httpMode: 'POST',
                url: 'https://discord.com/api/webhooks/1425012152946790433/G0koVM0hfMK2tvsr48OO7sPH7m2OvtZmmP3_urPVq_Njj-eD7Dfxeia5aOP8WnxqxATN',
                requestBody: "{\"content\": \"❌ Build Gagal untuk branch ${env.BRANCH_NAME}\"}",
                contentType: 'APPLICATION_JSON'
            )
        }
    }
}