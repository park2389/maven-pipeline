#!/usr/bin/env groovy

pipeline {
    agent any

    tools {
        maven 'mvn-3.5.4'
        jdk 'jdk-10.0.2'
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
                    deltaComplexityCoverage: '19',
                    deltaLineCoverage: '90'
            )

        }

    }
}