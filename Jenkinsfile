pipeline {
    agent { label 'jenkins-Agent' }
    
    tools {
        jdk 'java17'
        maven 'maven3'
    }

    stages {
        stage("Cleanup Workspace") {
            steps {
                cleanWs()
            }
        }
        
        stage("Checkout from SCM") {
            steps {
                git branch: 'main', credentialsId: 'github', url: 'https://github.com/Lokendrasaini/jenkins-cicd.git'
            }
        }
        
        stage("Build Application") {
            steps {
                sh "mvn clean package"
            }
        }
        
        stage("Test Application") {
            steps {
                sh "mvn test"
            }
        }
        
        stage("SonarQube Analysis") {
            steps {
                script {
                    withSonarQubeEnv('jenkins-sonarqube-token') {
                        sh "mvn sonar:sonar"
                    }
                }
            }
        }
        
        stage("Quality Gate") {
            steps {
                script {
                    def qualityGate = waitForQualityGate()
                    if (qualityGate.status != 'OK') {
                        error "Pipeline aborted due to quality gate failure: ${qualityGate.status}"
                    }
                }
            }
        }
    }
}

  
