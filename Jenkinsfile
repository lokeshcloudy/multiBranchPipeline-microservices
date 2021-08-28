@Library('JenkinsSharedLibrary')_
pipeline {
    agent any
    tools {
        gradle 'Gradle'
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
                    buildImage "lokeshlish/${BRANCH_NAME}:1.0.0"
                }
            }
        }
        stage("DockerPush") {
            steps {
                script {
                    dockerPush "lokeshlish/${BRANCH_NAME}:1.0.0"
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
