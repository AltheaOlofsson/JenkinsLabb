pipeline {
    agent any

    environment {
        gitUrl  =   "https://github.com/AltheaOlofsson/JenkinsLabb.git"
    }
    parameters {
        choice choices: ['main', 'b1'], description: 'Which Branch do you want to run?', name: 'Branch'
    }
    options {
        skipDefaultCheckout()
    }

    stages {       
        stage('Clean Jenkins Workspace') {
            steps {
                cleanWs()
            }
        } 
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
        stage('Trailrunner reports') {
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