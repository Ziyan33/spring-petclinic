pipeline {
    agent any

    triggers {
        cron('H/10 * * * 1')
    }

    stages {
        stage('Build') {
            steps {
                script {
                    // Use Maven to build the project. Adjust the command for Windows if necessary.
                    bat 'mvn clean package'
                }
            }
        }

        stage('Code Coverage') {
            steps {
                script {
                    // Generate code coverage report with Jacoco. Adjust the command for Windows if necessary.
                    bat 'mvn test jacoco:report'
                }
            }
        }
    }

    post {
        always {
            // Archive the build artifacts (e.g., JAR files)
            archiveArtifacts artifacts: '**/target/*.jar', fingerprint: true
            // Archive the Jacoco reports
            jacoco(
                execPattern: '**/target/jacoco.exec',
                classPattern: '**/classes',
                sourcePattern: '**/src/main/java',
                inclusionPattern: '**/*.*',
                exclusionPattern: ''
            )
            // Optionally, you could publish JUnit test results if you have them
            junit '**/target/surefire-reports/*.xml'
        }
    }
}
