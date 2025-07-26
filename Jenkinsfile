pipeline {
    agent any
    environment {
    SONAR_HOST = 'http://localhost:9000'
    SONAR_TOKEN = credentials('sonarqubetoken')
  }

    stages {

    stage('Clean Workspace') {
            steps {
                cleanWs()
            }
        }
    
        stage('Checkout') {
            steps {
                // git 'https://github.com/deopura/getting-started.git'
                git branch: 'main', url: 'https://github.com/deopura/getting-started.git'
          }
        }

  stage('SonarQube Analysis') {
            steps {
            withSonarQubeEnv('SonarQube') {
                script {
                def scannerHome = tool name: 'SonarScanner', type: 'hudson.plugins.sonar.SonarRunnerInstallation'
                sh "${scannerHome}/bin/sonar-scanner -Dsonar.projectKey=sonartest -Dsonar.sources=src"
                    // sh "${scannerHome}/bin/sonar-scanner"
                }
                }
            }
            }      

        stage('Build') {
            steps {
                echo 'Building..'
                // Check the docker-compose version
                sh 'docker compose version'
                // Bring up the services
                //sh 'docker compose up -d'               // Ensure the services are running
            }
        }

        stage('Test') {
            steps {
                echo 'Testing..'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
                sh 'docker compose ps'
            }
        }
    }
}