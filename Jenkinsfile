/* Requires the Docker Pipeline plugin */
// pipeline {
//     agent { docker { image 'python:3.12.1-alpine3.19' } }
//     stages {
//         stage('build') {
//             steps {
//                 sh 'python --version'
//             }
//         }
//     }
// }

pipeline {
    agent any
    stages {
        stage('No-op') {
            steps {
                sh 'exit 1'
            }
        }
    }
    post {
        always {
            echo 'One way or another, I have finished'
            deleteDir() /* clean up our workspace */
        }
        success {
            echo 'I succeeded!'
        }
        unstable {
            echo 'I am unstable :/'
        }
        failure {
            mail to: 'external.nicolas.caro@de.bosch.com',
            subject: "Failed Pipeline: ${currentBuild.fullDisplayName}",
            body: "Something is wrong with ${env.BUILD_URL}"
        }
        changed {
            echo 'Things were different before...'
        }
    }
}