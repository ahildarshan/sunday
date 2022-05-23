pipeline {
    agent any
    environment{
        MY_FILE = fileExists 'Software-Development'
        EMAIL_TO = 'diwakard158@gmail.com'
    }
    post {
        success {
            emailext body: 'Check console output at $BUILD_URL to view the results. \n\n ${CHANGES} \n\n -------------------------------------------------- \n${BUILD_LOG, maxLines=100, escapeHtml=false}',
                    to: "${EMAIL_TO}",
                    subject: 'Build succeeded in Jenkins: $PROJECT_NAME - #$BUILD_NUMBER'
        }
        failure {
            emailext body: 'Check console output at $BUILD_URL to view the results. \n\n ${CHANGES} \n\n -------------------------------------------------- \n${BUILD_LOG, maxLines=100, escapeHtml=false}',
                    to: "${EMAIL_TO}",
                    subject: 'Build failed in Jenkins: $PROJECT_NAME - #$BUILD_NUMBER'
        }
        unstable {
            emailext body: 'Check console output at $BUILD_URL to view the results. \n\n ${CHANGES} \n\n -------------------------------------------------- \n${BUILD_LOG, maxLines=100, escapeHtml=false}',
                    to: "${EMAIL_TO}",
                    subject: 'Unstable build in Jenkins: $PROJECT_NAME - #$BUILD_NUMBER'
        }
        changed {
            emailext body: 'Check console output at $BUILD_URL to view the results.',
                    to: "${EMAIL_TO}",
                    subject: 'Jenkins build is back to normal: $PROJECT_NAME - #$BUILD_NUMBER'
        }
    }
    stages {
        stage('clone repo') {
            when { expression { MY_FILE == 'false' } }
            steps {
 	            bat "git clone https://github.com/diwakarsrinivas/Software-Development.git"
 	            print "pulled the code"
            }
        }
        stage('Compile') {
            steps {
                bat """
                cd Software-Development
                mvn compile
                """
            }
        }
        stage('Test') {
            steps {
               bat"""
               cd Software-Development
               mvn test
               """
            }
        }
        stage('Package') {
            steps {
               bat"""
               cd Software-Development
               mvn package
               """
            }
        }
    }
}
