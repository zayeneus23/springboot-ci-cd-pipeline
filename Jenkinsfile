pipeline {
    agent any

    tools {
        maven 'Maven 3.8.6'   // Nom défini dans Manage Jenkins > Global Tool Configuration
        jdk 'JDK 17'          // Idem
    }

    environment {
        // Récupération du token stocké dans Jenkins Credentials (type Secret text, ID = sonar-token)
        SONAR_TOKEN = credentials('sonar-token')
        MAVEN_HOME = tool 'Maven 3.8.6'
        JAVA_HOME  = tool 'JDK 17'
        PATH       = "${JAVA_HOME}\\bin;${MAVEN_HOME}\\bin;${env.PATH}"
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/zayeneus23/springboot-ci-cd-pipeline.git'
            }
        }

        stage('Build Maven') {
            steps {
                bat 'mvn clean install'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('sonar') {
                    bat "mvn sonar:sonar -Dsonar.login=${SONAR_TOKEN}"
                }
            }
        }

        stage('Docker Build') {
            steps {
                // Vérifie que Docker est installé et accessible sur l'agent
                bat 'docker --version'
                // Construit l'image Docker
                bat 'docker build -t springboot-app .'
            }
        }
    }

    post {
        success {
            echo '✅ Pipeline CI/CD exécuté avec succès !'
        }
        failure {
            echo '❌ Une erreur est survenue dans le pipeline.'
        }
    }
}
