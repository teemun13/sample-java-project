pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                echo 'Checking out source code'
                git branch: 'master', url: 'https://github.com/yyxxxy/sample-java-project.git'
            }
        }
        stage('Build') {
            steps {
                echo 'Running Gradle build'
                powershell 'gradle --no-daemon clean build'
            }
        }
        stage('Test') {
            steps {
                echo 'Running Gradle tests'
                powershell 'gradle --no-daemon test'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying application'
                script {
                    def jarFile = 'build/libs/SCC.jar'
                    if (fileExists(jarFile)) {
                        powershell "java -jar ${jarFile}"
                    } else {
                        error "JAR file not found: ${jarFile}"
                    }
                }
            }
        }
    }
    post {
        always {
            echo 'Cleaning up workspace'
            deleteDir() // Clean up the workspace after the build
        }
        success {
            echo 'Build succeeded!!!'
            // You could add notification steps here
        }
        failure {
            echo 'Build failed!'
            // You could add notification steps here
        }
    }
}
