#!/usr/bin/env groovy

pipeline {
    agent any

    tools {
        maven 'Maven 3.6.1'
        jdk 'jdk 1.8.0'
    }

    stages {
        stage('Build') {
            steps {
                sh "printenv"
                sh "mvn clean test package spring-boot:repackage"

            }
        }

    }
    post {
        always{
//            junit 'target/surefire-reports/**/*.xml'
            junit(testResults: '**/target/surefire-reports/**/*.xml')
            jacoco(
                    execPattern: 'target/**/*.exec',
                    classPattern: 'target/classes',
                    sourcePattern: 'src/main/java',
                    exclusionPattern: 'src/test*',
                    buildOverBuild: true,
                    changeBuildStatus: true,
                    deltaLineCoverage: '69',
                    minimumLineCoverage:'0',
                    maximumLineCoverage: '61'
            )

        }

    }
}
