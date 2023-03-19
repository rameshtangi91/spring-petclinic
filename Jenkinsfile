
pipeline {
    agent { label 'node1' }
    triggers {
        pollSCM ('* * * * *')
    }
    parameters {
        choice(name:'MAVEN_GOAL' choices: ['package', 'install', 'clean'], description: 'maven-goal')
    }
    stages { 
        stage('version control system') {
            steps {
                git url: 'https://github.com/rameshtangi91/spring-petclinic.git',
                    branch: 'main'
            }
        }
        stage('package') {
            tools {
                jdk 'JDK_17'
            }
            steps {
                sh "mvn ${params.MAVEN_GOAL}"
            }
        }
         stage('post build') {
            steps {
                archiveArtifacts artifacts: '**/target/spring-petclinic-3.0.0-SNAPSHOT.jar',
                                 onlyIfSuccessful: true
                junit testResults: '**/surefire-reports/TEST-*.xml'                 
            }
        }
    }
}