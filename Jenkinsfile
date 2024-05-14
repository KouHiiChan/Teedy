pipeline {
    agent any
    
    environment {
        DOCKER_HUB_CREDENTIALS = credentials('cs304-lab12')
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scmGit(branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url: 'git@github.com:KouHiiChan/Teedy.git']])
            }
        }

        stage('Build') {
            steps {
                sh 'mvn -B -DskipTests clean package'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    dockerImage = docker.build("kohiichan/cs304lab12:${env.BUILD_NUMBER}", "Dockerfile")
                }
            }
        }

        // stage('Push Docker Image') {
        //     steps {
        //         script {
        //             docker.withRegistry('', DOCKER_HUB_CREDENTIALS) {
        //                 dockerImage.push()
        //             }
        //         }
        //     }
        // }

        post {
            always {
                archiveArtifacts artifacts: '**/target/site/**', fingerprint: true
                archiveArtifacts artifacts: '**/target/**/*.jar', fingerprint: true
                archiveArtifacts artifacts: '**/target/**/*.war', fingerprint: true
            }
        }

    }
}
