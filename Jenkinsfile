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
                    bat 'mvn clean install'
                }
            }
        }
        stage('Test TrailRunner') {
            steps {
                dir('TrailrunnerProject') {
                        bat 'mvn test'
                }
                [12:02] Hamid Hosseini - Utbildare
stage('Post Test') {

            steps {

                script {

                    jacoco(
                        execPattern: 'target/*.exec',
                        classPattern: 'target/classes',
                        sourcePattern: 'src/main/java',
                        exclusionPattern: 'src/test*'
                    )
                    junit '**/TEST*.xml'

                }

            }

        }

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