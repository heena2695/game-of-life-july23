pipeline {
    agent { label 'GOL' }
    options {
        timeout(time: 10, unit: 'MINUTES') 
    }
    triggers { pollSCM('5 * * * *') }
    tools {
        jdk 'JAVA_8'
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
                sh 'mvn compile'

            } 
        }
        
    }
}