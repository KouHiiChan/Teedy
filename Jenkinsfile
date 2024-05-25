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

        // stage('Build Docker Image') {
        //     steps {
        //         sh 'docker build -t lab12 .'
        //     }
        // }

        // stage('Push Docker Image') {
        //     steps {
        //         // sh 'docker login -u kohiichan -p hgyToLOVEru=7'
        //         sh 'docker tag lab12 kohiichan/lab12_v1.0'
        //         sh 'docker push kohiichan/lab12_v1.0'
        //     }
        // }

        // stage('Run containers'){
        //     steps{
        //         sh 'docker pull kohiichan/lab12_v1.0:latest'
        //         sh 'docker stop 1201'
        //         // sh 'docker stop 1202'
        //         // sh 'docker stop 1203'
        //         sh 'docker rm 1201'
        //         // sh 'docker rm 1202'
        //         // sh 'docker rm 1203'
        //         sh 'docker run -d -p 8082:8080 --name 1201 kohiichan/lab12_v1.0'
        //         // sh 'docker run -d -p 8083:8080 --name 1202 kohiichan/lab12_v1.0'
        //         // sh 'docker run -d -p 8084:8080 --name 1203 kohiichan/lab12_v1.0'
        //         // sh 'docker start 1201'
        //         // sh 'docker start 1202'
        //         // sh 'docker start 1203'
        //     }
        // }

        stage('K8s') {
            steps {
                sh 'docker stop 1201'
                sh 'docker rm 1201'
                sh 'docker run -d -p 8082:8080 --name 1201 kohiichan/lab12_v1.0'
                sh 'kubectl set image deployments/hello-node 1201=kohiichan/lab12_v1.0:latest'
            }
        }

    }

    // post {
    //         always {
    //             archiveArtifacts artifacts: '**/target/site/**', fingerprint: true
    //             archiveArtifacts artifacts: '**/target/**/*.jar', fingerprint: true
    //             archiveArtifacts artifacts: '**/target/**/*.war', fingerprint: true
    //         }
    //     }
}
