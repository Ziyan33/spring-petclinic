pipeline {
    agent any

    triggers {
        cron('H/10 * * * 1')
    }

    stages {
        stage('Build') {
            steps {
                script {
                    // Use Maven to build the project
                    sh 'mvn clean package'
                }
            }
        }

        stage('Code Coverage') {
            steps {
                script {
                    // Generate code coverage report with Jacoco
                    sh 'mvn test jacoco:report'
                }
            }
        }
    }

    post {
        always {
            // Archive the artifacts and reports
            archiveArtifacts artifacts: '**/target/*.jar', fingerprint: true
            junit '**/target/surefire-reports/*.xml'
            jacoco execPattern: '**/target/jacoco.exec'
        }
    }
}
