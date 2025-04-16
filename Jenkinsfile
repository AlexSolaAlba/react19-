pipeline {
    agent any

    triggers {
        cron('H H * * *') // Build diario
    }

    stages {
        stage('Instalar dependencias') {
            steps {
                sh 'npm install --force || true'
            }
        }

        stage('Ejecutar pruebas y generar cobertura') {
            steps {
                sh 'npx jest --coverage'
            }
        }

        stage('Publicar reporte de cobertura') {
            steps {
                publishHTML([
                    allowMissing: true,
                    alwaysLinkToLastBuild: true,
                    keepAll: true,
                    reportDir: 'coverage/lcov-report',
                    reportFiles: 'index.html',
                    reportName: 'Cobertura de Código'
                ])
            }
        }
    }

    post {
        success {
            echo '✅ Pruebas y cobertura ejecutadas correctamente.'
        }
        failure {
            echo '❌ Error durante la ejecución de pruebas o cobertura.'
        }
    }
}
