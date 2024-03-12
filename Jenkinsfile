pipeline {
    agent any
    environment {
        gitURL  =   "https://github.com/AltheaOlofsson/JenkinsLabb.git"
    }
    parameters {
        choice choices: ['main', 'b1'], description: 'Which Branch do you want to run?', name: 'Branch'
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: "${params.Branch}", url: "${gitURL}"
            }
        }
        stage('Build TrailRunner') {
            steps {
                dir('TrailrunnerProject') {
                    bat 'mvn compile'
                }
            }
        }
        stage('Stage3') {
            steps {
                echo 'Stage 3'
            }
        }
        stage('Stage4') {
            steps {
                echo 'Stage 4'
            }
            post { 
                always { 
                    echo 'Post stage 4'
                }
            }
        }
        
    }
}