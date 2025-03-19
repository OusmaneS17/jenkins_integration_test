pipeline {
    agent any

    environment {
        PYTHON_EXE="C:\\Users\\o.sow\\AppData\\Local\\Programs\\Python\\Python312\\python.exe"
        VENV_DIR= 'venv'
    }

    stages {
        stage('recup code github') {
            steps {
                git branch: 'main', url: 'https://github.com/OusmaneS17/jenkins_integration_test.git'
            }
        }

        stage('Installation des dependances') {
            steps {
                bat '%PYTHON_EXE% -m venv %VENV_DIR%'
            }
        }

        stage('compiler le script') {
            steps {
                bat '%VENV_DIR%\\Scripts\\python app.py'
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
