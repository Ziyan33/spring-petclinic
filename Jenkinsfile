pipeline {
    agent any

    triggers {
        cron('H 10 * * 1') // Trigger every 10 minutes on Monday
    }

    stages {
        stage('Build and Test') {
            steps {
                bat 'git clone https://github.com/[your-github-username]/spring-petclinic.git'
                bat 'mvn clean package'
                jacoco()
            }
        }
    }

   post {
       always {
           publishHTML([allowMissing: false, alwaysLinkToLastBuild: false, keepAll: true, reportDir: 'target/site/jacoco', reportFiles: 'index.html', reportNames: 'Jacoco Code Coverage Report', reportTitles: 'Petclinic'])
       }
   }

}
