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
