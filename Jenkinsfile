pipeline {
    agent {
        label 'linux'
    }

    options {
        timestamps()
        disableConcurrentBuilds(abortPrevious: true)
        timeout(time: 1, unit: 'HOURS')
    }

    stages {
        stage('build dev JeeExamples') {
            steps {
                // build
                withMaven(globalMavenSettingsConfig: 'ae44f8b3-3bf7-4624-8e87-74659f3f817f', maven: 'maven3', traceability: true) {
                    sh "mvn clean install"
                }
                recordIssues(tools: [mavenConsole()])
            }
        }
    }

    post {
        aborted {
            // Email senden
            script {
                try {
                    echo "email sent"
                    throw new Exception()
                } catch(Exception e) {
                    e.printStackTrace()
                } finally {
                    echo "noch mal gut gegangen, ... oder nicht?"
                }
            }
        }
        success {
            // clean ws
            cleanWs notFailBuild: true
        }
        failure {
            // Log Files an server senden
            echo "log files transmitted"
        }
    }
}