pipeline {
    agent any
    environment {
        gitURL  =   "https://github.com/AltheaOlofsson/JenkinsLabb.git"
    }
    parameters {
        choice choices: ['main', 'B1'], description: "Choose which branch to run", name: "Branch"
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: params.Branch, url: "${gitURL}"
            }
        }
        stage('Stage2') {
            steps {
                echo 'Stage 2'
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