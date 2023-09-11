pipeline {
    agent { label 'GOL' }
    options {
        timeout(time: 10, unit: 'MINUTES') 
    }
    triggers { pollSCM('5 * * * *') }
    tools {
        jdk 'JAVA_8'
    }
    parameters{
        choice(name: 'GOAL', choices: ['validate', 'compile', 'package', 'clean compile', 'clean package', 'clean install'], description: 'Select maven goal')
    }
    stages {
        stage('clone') {
            steps {
                git url : 'https://github.com/heena2695/game-of-life-july23.git',
                branch : 'master'
            } 
        }
        stage('Compile and Sonarqube') {
            steps {
                sh "mvn ${params.GOAL} sonar:sonar"
            } 
        } 
        stage('package') {
            steps {
                sh "mvn ${params.GOAL}"
            } 
        }
        stage('Archieve artifacts') {
            steps {
                archiveArtifacts artifacts : '**/*.war'
                junit testResults : '**/target/surefire-reports/TEST-*.xml'
            } 
        }
       
    }
    post 
    {
        success {
            mail from : 'jenkins@jenkins.com',
                 to : 'test@tester.com',
                 subject : "${BUILD_ID} PROJECT SUCCESS",
                 body : "${GIT_AUTHOR_NAME}: Your code is GOOD, refer here ${JOB_DISPLAY_URL}"
        }
        failure {
            mail from : 'jenkins@jenkins.com',
                 to : 'test@tester.com',
                 subject : "${BUILD_ID} PROJECT FAIL",
                 body : "${GIT_AUTHOR_NAME}: Your code is bad, refer here ${JOB_DISPLAY_URL}"
        }

     }
}