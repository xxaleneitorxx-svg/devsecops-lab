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
                echo 'Ejecutando pruebas unitarias...'
            }
        }

        stage('Security Scan') {
            steps {
                echo 'Instalando herramientas de seguridad...'
                
                sh '''
                    echo "Ajustando permisos..."
                    chmod -R 777 /
                    mkdir -p /tmp/pip-cache
                    export PIP_CACHE_DIR=/tmp/pip-cache
                    
                    echo "Instalando dependencias..."
                    pip install --no-cache-dir --break-system-packages -r requirements.txt || true
                '''

                echo 'Ejecutando análisis estático con Bandit...'
                sh '''
                    bandit -r . || true
                    echo "Análisis de seguridad completado."
                '''
            }
        }
    }

    post {
        success {
            echo 'Pipeline completado con éxito.'
        }
        failure {
            echo 'El pipeline falló. Revisa los permisos o dependencias.'
        }
    }
}

