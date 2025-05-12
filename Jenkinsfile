pipeline {
    agent any

    tools {
        maven 'Maven 3.8.6'   // Corrigé ici
        jdk 'JDK 17'          // Assure-toi que ce nom existe aussi dans Jenkins
    }

    environment {
        MAVEN_HOME = tool 'Maven 3.8.6'
        JAVA_HOME = tool 'JDK 17'
        PATH = "${JAVA_HOME}/bin:${MAVEN_HOME}/bin:${env.PATH}"
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/zayeneus23/springboot-ci-cd-pipeline.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean compile'
            }
        }

        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }

        stage('Package') {
            steps {
                sh 'mvn package'
            }
        }
    }

    post {
        success {
            echo '✅ Build réussi !'
        }
        failure {
            echo '❌ Le build a échoué.'
        }
    }
}
