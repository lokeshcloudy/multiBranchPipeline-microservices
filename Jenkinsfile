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
    environment {
        BRANCH_NAME = "${GIT_BRANCH.split("/").size() > 1 ? GIT_BRANCH.split("/")[1] : GIT_BRANCH}"
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
                    buildImage "lokeshlish"
                }
            }
        }
        stage("DockerPush") {
            steps {
                script {
                    dockerPush "lokeshlish"
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
