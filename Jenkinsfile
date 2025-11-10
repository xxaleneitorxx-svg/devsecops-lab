pipeline {
    agent { docker { image 'python:3.9-slim' } }

    stages {
        stage('Build') {
            steps {
                echo 'Construyendo el proyecto...'
            }
        }

        stage('Test') {
            steps {
                echo 'Ejecutando pruebas...'
            }
        }

        stage('Security Scan') {
            steps {
                echo 'Instalando herramientas de seguridad...'
                sh '''
                    export HOME=/tmp
                    pip install --no-cache-dir --user -r requirements.txt
                '''

                echo 'Ejecutando análisis estático con Bandit...'
                sh '''
                    export HOME=/tmp
                    ~/.local/bin/bandit -r . || true
                '''
            }
        }
    }
}
