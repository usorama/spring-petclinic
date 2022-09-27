pipeline {
    agent {label 'NODE2-JDK11-MVN'}
    parameters {
        choice(name: 'BRANCH_TO_BUILD', choices: ['JenkinsTest', 'main'], description: 'Branch to build')
        string(name: 'MAVEN_GOAL', defaultValue: 'mvn package', description: 'Maven Goal')
    }
    stages {
        stage('get') {
            steps {
                git branch: "${params.BRANCH_TO_BUILD}", url: 'https://github.com/usorama/spring-petclinic.git'
            }
        }
        stage('build') {
            steps {
                sh "${params.MAVEN_GOAL}"
            }
        }
        stage('Archive test results') {
            steps {
                junit '**/surefire-reports/*.xml'
            }
        }
        stage('Archive artifacts') {
            steps {
            archive '**/target/*.jar'
            }
        }
    }    
}