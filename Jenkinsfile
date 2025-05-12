pipeline {
    agent any

    tools {
        jdk 'JDK 17'       // Doit correspondre au nom que tu as mis dans "Global Tool Configuration"
        maven 'Maven 3.8.6' // Idem
    }

   stage('Checkout') {
    steps {
        git branch: 'main', url: 'https://github.com/zayeneus23/springboot-ci-cd-pipeline.git'
    }
}

        stage('Build') {
            steps {
                sh 'mvn clean install'
            }
        }

        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }
    }
}
