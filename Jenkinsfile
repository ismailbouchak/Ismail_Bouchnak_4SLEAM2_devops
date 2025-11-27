pipeline {
    agent any
environment {
        DOCKER_CREDENTIALS= credentials('63f7ba37-5357-4448-98a3-6490f139b7a1')
    }
    tools {
        jdk 'JAVA_HOME'
        maven 'M2_HOME'
    }

    environment {
        GIT_CREDENTIALS = 'Sudo_Git'
    }

    stages {

        stage('Clone Project') {
            steps {
                git branch: 'main',
                    credentialsId: "${GIT_CREDENTIALS}",
                    url: 'https://github.com/ismailbouchak/Ismail_Bouchnak_4SLEAM2_devops.git'
            }
        }

        stage('Build: clean & package') {
            steps {
                sh 'mvn clean package -DskipTests'
                echo 'Build finished! JAR is available in target/.'
            }
        }
        stage('Docker Build') {
            steps {
                script {
                    sh "docker build -t DockerAccountUsername/student-management:1.0 ."
                }
            }
        }

        stage('Docker Push') {
            steps {
                script {
                    sh 'echo $DOCKER_CREDENTIALS_PSW | docker login -u $DOCKER_CREDENTIALS_USR --password-stdin'
                    sh "docker push DockerAccountUsername/student-management:1.0"
                }
            }

    }
}
