pipeline {
    agent any

    tools {
        jdk 'java_17'
        maven 'maven'
    }

    environment {
        GIT_CREDENTIALS = 'Sudo_Git'
    }

    stages {

        stage('Clone Project') {
            steps {
                git branch: 'main',
                    credentialsId: "${GIT_CREDENTIALS}",
                    url: 'https://github.com/oussama56159/touati_oussama4Sleam2.git'
            }
        }

        stage('Build: clean & package') {
            steps {
                sh 'mvn clean package -DskipTests'
                echo 'Build finished! JAR is available in target/.'
            }
        }

    }
}
