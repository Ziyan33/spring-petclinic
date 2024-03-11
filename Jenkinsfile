pipeline {
    agent any

    triggers {
        cron('H/10 * * * 1')
    }



 stages {
        stage('Initialize') {
            steps {
                echo 'Initializing...'
            }
        }

        stage('Build') {
            steps {
                echo 'Building...'
                bat 'mvn clean package -DskipTests'
            }
        }

        stage('Test') {
            steps {
                echo 'Testing...'
                bat 'mvn test'
            }
        }

        stage('Generate Jacoco Report') {
            steps {
                echo 'Generating Jacoco Coverage Report...'
                bat 'mvn jacoco:report'
            }
        }
    }

    post {
        always {
            echo 'Pipeline execution is complete.'
        }
    }
}
