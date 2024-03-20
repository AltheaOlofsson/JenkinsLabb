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
                catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                    bat 'mvn test'
                    script {
                        try {
                        bat 'mvn test'
                        }catch (e) {
                            mail to: 'althea.olofsson@gmail.com',
                            subject: "Failed Pipeline: ${currentBuild.fullDisplayName}",
                            body: "Something is wrong with ${env.BUILD_URL}"
                            throw e
                        }
                    }
                }
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
                catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                    script {
                        try {
                        bat 'robot  --variable browser:headlesschrome --outputdir RobotResults BokaBil.robot'
                        }catch (e) {
                            mail to: 'althea.olofsson@gmail.com',
                            subject: "Failed Pipeline: ${currentBuild.fullDisplayName}",
                            body: "Something is wrong with ${env.BUILD_URL}"
                            throw e
                        }
                    }
                }
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
    post {
        failure {
            mail to: 'althea.olofsson@gmail.com',
                subject: "Failed Pipeline: ${currentBuild.fullDisplayName}",
                body: "Something is wrong with ${env.BUILD_URL}"
        }
    }
}
