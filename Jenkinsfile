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
        stage("DockerBuild") {
            steps {
                script {
                    buildImage "lokeshlish/env.BRANCH_NAME"
                }
            }
        }
        stage("DockerPush") {
            steps {
                script {
                    dockerPush "lokeshlish/env.BRANCH_NAME"
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
