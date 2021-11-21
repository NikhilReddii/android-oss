pipeline {
    agent any
    options {
        buildDiscarder(logRotator(daysToKeepStr:'30'))
        ansiColor('xterm')
    }
    stages {
        stage('Fetching-Required-Lines') {
            steps {
                script {
                    try {
                        sh '''#!/bin/bash
                            sed -n '14p; 16p' inputFile
                        '''
                    }
                    catch (Exception e) {
                        echo e.toString()
                        sh 'exit 1'
                    }
                }
            }         
        }
    }
    post {
        always {
            script {
                    try {
                        wrap([$class: 'BuildUser']) {
                            currentBuild.displayName  = "#${BUILD_NUMBER}-${BUILD_USER}"
                        }
                    } 
                     catch (Exception e) {
                        echo e.toString()
                        sh 'exit 1'
                    }
            }
        }
    }
}
