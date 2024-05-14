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
                sh 'docker build -t lab12 .'
            }
        }

        stage('Push Docker Image') {
            steps {
                // sh 'docker login -u kohiichan -p hgyToLOVEru=7'
                sh 'docker tag lab12 kohiichan/lab12_v1.0'
                sh 'docker push kohiichan/lab12_v1.0'
            }
        }

    }

    post {
            always {
                archiveArtifacts artifacts: '**/target/site/**', fingerprint: true
                archiveArtifacts artifacts: '**/target/**/*.jar', fingerprint: true
                archiveArtifacts artifacts: '**/target/**/*.war', fingerprint: true
            }
        }
}
