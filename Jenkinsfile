pipeline {
    agent any
    
    stages {
        stage('Back-end') {
            agent {
                docker {
                    image 'maven:3.8.1-adoptopenjdk-11'
                }
            }
            steps {
                sh 'mvn --version'
            }
        }
        
        stage('Front-end') {
            agent {
                docker {
                    image 'node:16-alpine'
                }
            }
            steps {
                sh 'node --version'
                sh 'npm install' // Install front-end dependencies
                sh 'npm run build' // Build your front-end application
                sh 'npm start' // Run your front-end application
            }
        }
        
        stage('Database') {
            agent {
                docker {
                    image 'mysql:latest' // Replace with your database image
                }
            }
            steps {
                sh 'docker run -d -p 5432:5432 mysql:latest' // Start the database container
                sleep time: 30, unit: 'SECONDS' // Wait for the database to start
            }
        }
    }
}
