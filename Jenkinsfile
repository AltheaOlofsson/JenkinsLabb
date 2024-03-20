pipeline {
    agent any

    stages {       

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
