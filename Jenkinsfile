pipeline {
    agent any

    tools {
        jdk 'JAVA_HOME'
        maven 'M2_HOME'
    }

    environment {
        GIT_CREDENTIALS = 'Sudo_Git'
        DOCKER_CREDENTIALS_USR = credentials('63f7ba37-5357-4448-98a3-6490f139b7a1')
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
        stage('Docker Push') {
        steps {
            script {
                sh "echo ${DOCKER_CREDENTIALS_USR_PSW} | docker login -u ismail4000 --password-stdin"
                sh "docker push ismail4000/student-management:1.0"
            }
        }
    }
    stage('Docker Build') {
        steps {
            script {
                sh "docker build -t ismail4000/student-management:1.0 ."
            }
        }
    }

    }
}
