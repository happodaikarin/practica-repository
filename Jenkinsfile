pipeline {
    agent any
    tools {
        maven "Maven"  // Nombre de la configuración de Maven en Jenkins
        jdk "JDK17"    // Nombre de la configuración de JDK en Jenkins
    }
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/happodaikarin/practica-repository.git'
            }
        }
        stage('Build') {
            steps {
                sh 'mvn clean compile'
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test'  // Si tienes pruebas unitarias
            }
        }
        stage('Deploy') {
            steps {
                sh 'mvn package'  // Genera el JAR en target/
                archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
            }
        }
    }
    post {
        success {
            emailext (
                subject: '✅ Build exitoso',
                body: 'El build de Hola Mundo Java fue exitoso.',
                to: 'tu-email@empresa.com'
            )
        }
        failure {
            emailext (
                subject: '❌ Build fallido',
                body: 'El build de Hola Mundo Java falló. Ver logs: ${BUILD_URL}',
                to: 'tu-email@empresa.com'
            )
        }
    }
}
