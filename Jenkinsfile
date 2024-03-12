pipeline {
    agent any
    stages {
        stage('Stage1') {
            steps {
                echo 'Hello World'
            }
        }
        stage('Stage2') {
            steps {
                echo 'Hello World'
            }
        }
        stage('Stage3') {
            steps {
                echo 'Hello World'
            }
        }
        stage('Stage4') {
            steps {
                echo 'Hello World'
            }
            post { 
                always { 
                    echo 'I will always say Hello again!'
                }
            }
        }
        
    }
}