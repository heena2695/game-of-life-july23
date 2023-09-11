pipeline {
    agent { label 'GOL' }
    options {
        timeout(time: 10, unit: 'MIN') 
    }
    triggers { pollSCM('5 * * * *') }
    tools {
        jdk 'JDK-8'
    }
    stages {
        stage('src') {
            steps {
                git url : 'https://github.com/heena2695/game-of-life-july23.git',
                branch : 'master'

            } 
        }
        stage('build') {
            steps {
                sh 'mvn validate'

            } 
        }
        
    }
}