#!/usr/bin/env groovy

library identifier: 'JenkinsSharedLibrary@main', retriever: modernSCM(
        [$class: 'GitSCMSource',
         remote: 'https://github.com/lokeshcloudy/JenkinsSharedLibrary.git',
         credentialsId: 'github'
        ]
)_
pipeline {
    environment {
        BRANCH_NAME = "${GIT_BRANCH.split("/)[1]}"
    }
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
