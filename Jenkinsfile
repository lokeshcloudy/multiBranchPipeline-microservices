#!/usr/bin/env groovy

library identifier: 'JenkinsSharedLibrary@main', retriever: modernSCM(
        [$class: 'GitSCMSource',
         remote: 'https://github.com/lokeshcloudy/JenkinsSharedLibrary.git',
         credentialsId: 'github'
        ]
)_
pipeline {
    agent any
    tools {
        gradle 'Gradle'
        maven 'maven'
    }
    stages {
        stage("DockerLogin") {
            steps {
                script {
                    dockerLogin 'dockerhub'
                }
            }
        }
        stage("env") {
            steps {
                script {
                    sh 'printenv'
                }
            }
        }
        stage("DockerBuild") {
            steps {
                script {
                    buildImage 'lokeshlish'
                }
            }
        }
        stage("DockerPush") {
            steps {
                script {
                    dockerPush 'lokeshlish'
                }
            }
        }
        stage("Deploy") {
            steps {
                script {
                    deployApp()
                }
            }
        }
        
    }
}
