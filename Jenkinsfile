pipeline {
    agent any

    stages {
        stage('recup code github') {
            steps {
                git branch: 'main', url: 'https://github.com/OusmaneS17/jenkins_integration_test.git'
            }
        }

        stage('Installation des dependances') {
            steps {
                bat 'python -m venv venv'
            }
        }

        stage('compiler le script') {
            steps {
                bat '.\\venv\\Scripts\\python app.py'
            }
        }
    }

    post {
        success {
            emailext(
                subject: "Build SUCCESS: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                body: "Le build de ${env.JOB_NAME} a réussi.\nConsultez les logs ici: ${env.BUILD_URL}",
                recipientProviders: [[$class: 'DevelopersRecipientProvider']],
                to: 'oussoumanesow0@gmail.com'
            )
        }

        failure {
            emailext(
                subject: "Build FAILURE: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                body: "Le build de ${env.JOB_NAME} a échoué.\nConsultez les logs ici: ${env.BUILD_URL}",
                recipientProviders: [[$class: 'DevelopersRecipientProvider']],
                to: 'oussoumanesow0@gmail.com'
            )
        }
    }
}
