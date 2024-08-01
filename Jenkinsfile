pipeline {
    agent any

    environment {
        DESTINATION_DIR = '/var/www/html' // Cambia esto a la ubicación deseada para Nginx
    }

    triggers {
        pollSCM('H/5 * * * *') // Verificar el repositorio cada 5 minutos
    }

    stages {
        stage('Clonar repositorio') {
            steps {
                git 'https://github.com/DavidZomber935/Prueba-ISI-2024.git' 
            }
        }

        stage('Mover proyecto') {
            steps {
                script {
                    // Crear el directorio si no existe
                    sh "mkdir -p ${env.DESTINATION_DIR}"
                    
                    // Mover todos los archivos del proyecto a la ubicación de Nginx
                    sh "cp -r * ${env.DESTINATION_DIR}"
                }
            }
        }
    }

    post {
        success {
            echo 'Pipeline completado con éxito.'
        }
        failure {
            echo 'Pipeline falló.'
        }
    }
}
