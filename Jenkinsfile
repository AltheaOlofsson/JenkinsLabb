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
            }
        }
        stage('Post Test') {
            steps {
                script {
                    jacoco(
                        execPattern: '**/target/jacoco.exec',
                        classPattern: '**/target/classes/se/iths',
                        sourcePattern: '**/src/main/java/se/iths'
                    )
                    junit '**/TEST*.xml'
                }
            }
        }
        stage('Run Robot Framework') {
            steps {
                dir('Selenium') {
                    bat 'robot  --variable browser:headlesschrome --outputdir RobotResults BokaBil.robot'
                }
            }
        }
        stage('RobotResult') {
            steps {
                dir('Selenium') {
                    robot outputPath: 'RobotResults'
                }
            }
        } 
    }
}