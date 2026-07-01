pipeline {
    agent {
        node {
            label 'Docker'
        }
    }
    
    tools {
        maven 'Maven'
    }
    
    stages {
        stage('Source Code Checkout') {
            steps {
                git 'https://github.com/Rajaneesh2307/JAVA-DOCKER-ACCOUNT-WEBAPP.git'
            }
        }
        stage('Static Code Analysis (SonarQube)') {
            steps {
                withSonarQubeEnv('SonarQube-Scanner') {
                    sh "mvn clean verify sonar:sonar -Dsonar.projectKey=Java-Fullstack-Web-Application"
                }
            }
        }
        stage('Quality Gate Validation') {
            steps {
                timeout(time: 5, unit: 'MINUTES') {
                    waitForQualityGate abortPipeline: true
                }
            }
        }
        stage('Build & Package Artifact') {
            steps {
                sh 'mvn clean package'
                sh 'cp target/vprofile-v2.war Docker-app'
            }
        }
        stage('Upload Artifact to Nexus Repository') {
            steps {
                nexusArtifactUploader artifacts: [[artifactId: 'vprofile', classifier: '', file: 'target/vprofile-v2.war', type: 'war']], 
                    credentialsId: 'Nexus', groupId: 'com.visualpathit', nexusUrl: 'http://34.207.104.237:8081', nexusVersion: 'nexus3', protocol: 'http', repository: 'Java-Fullstack-Web-Application', version: 'v2'
            }
        }
        stage('Docker Image Build (App & DB)') {
            steps {
                sh 'docker build -t yembulururajaneesh/java-fullstack-web-application:db Docker-db'
                sh 'docker build -t yembulururajaneesh/java-fullstack-web-application:app Docker-app'
            }
        }
        stage('Container Image Security Scan (Trivy)') {
            steps {
                sh 'trivy image yembulururajaneesh/java-fullstack-web-application:db'
                sh 'trivy image yembulururajaneesh/java-fullstack-web-application:app'
            }
        }
        stage('Push Docker Images to Registry') {
            steps {
                script {
                    withDockerRegistry(credentialsId: 'DockerHub') {
                        sh 'docker push yembulururajaneesh/java-fullstack-web-application:db'
                        sh 'docker push yembulururajaneesh/java-fullstack-web-application:app'
                    }
                }
            }
        }
        stage('Deploy Application Stack to Docker Swarm') {
            steps {
                sh 'docker stack deploy -c docker-compose.yml ourstack'
            }
        }
    }
    post {
        always {
            emailext (
                to: '$DEFAULT_RECIPIENTS',
                subject: '$DEFAULT_SUBJECT',
                body: '$DEFAULT_CONTENT'
            )
        }
    }
}
