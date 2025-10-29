pipeline {
    agent {
        docker {
            image 'python:3.10'
            args '-u root'
        }
    }

    stages {
        stage('Checkout') {
            steps {
                echo "Checkout branch ${env.BRANCH_NAME}"
            }
        }

        stage('Install Dependencies') {
            steps {
                echo "Installing dependencies..."
                sh 'pip install -r requirements.txt'
            }
        }

        stage('Run Tests') {
            steps {
                echo "Menjalankan tes..."
                // Force gagal untuk testing
                sh 'exit 1'
            }
        }

        stage('Deploy') {
            when {
                anyOf {
                    branch 'main'
                    branch pattern: "release/.*", comparator: "REGEXP"
                }
            }
            steps {
                echo "Simulasi deploy dari branch ${env.BRANCH_NAME}"
            }
        }
    }

    post {
        success {
            script {
                def payload = [
                    content: "✅ Build SUCCESS di `${env.BRANCH_NAME}`\n🔗URL: ${env.BUILD_URL}"
                ]
                httpRequest(
                    httpMode: 'POST',
                    contentType: 'APPLICATION_JSON',
                    requestBody: groovy.json.JsonOutput.toJson(payload),
                    url: 'https://discord.com/api/webhooks/1429036405748666368/4aXIlhBtopqkzPu2Z3d0LVu-qzl3cPADzCtjZO2COQ2w6VD1pON41aQfQh5LV8VDZOaQ'
                )
            }
        }

        failure {
            script {
                def payload = [
                    content: "❌ Build FAILED di `${env.BRANCH_NAME}`\n🔗URL: ${env.BUILD_URL}"
                ]
                httpRequest(
                    httpMode: 'POST',
                    contentType: 'APPLICATION_JSON',
                    requestBody: groovy.json.JsonOutput.toJson(payload),
                    url: 'https://discord.com/api/webhooks/1429036405748666368/4aXIlhBtopqkzPu2Z3d0LVu-qzl3cPADzCtjZO2COQ2w6VD1pON41aQfQh5LV8VDZOaQ'
                )
            }
        }
    }
}
