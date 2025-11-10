pipeline {
    // Usamos un agente que tenga Python 3 y pip
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
                // Instala Flask y Bandit
                sh 'pip install -r requirements.txt'

                echo 'Ejecutando análisis estático con Bandit...'
                // Analiza el código Python y genera reporte
                sh 'bandit -r . || true'
            }
        }
    }
}
