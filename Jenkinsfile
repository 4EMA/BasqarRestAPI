pipeline {
    agent any

    stages {
        stage('pull stage') {
            steps {
                git branch: 'master',
                url: 'https://github.com/4EMA/BasqarRestAPI.git'
            }
        }
        stage('test  stage') {
            steps {
                sh "mvn -Dmaven.test.failure.ignore=true  test"
            }
        }
        stage('result stage') {
            steps {
               step([$class: 'Publisher', reportFilenamePattern: '**/testng-results.xml'])
            }
       post {
                success {
                    telegramSend "Build was successfull, link: ${BUILD_URL}"
                }
                failure {
                    telegramSend "Build was failure, link: ${BUILD_URL}"
                }
                unstable {
                    telegramSend "Build was unstable, link: ${BUILD_URL}"
                }
            }
        }
        stage('echo stage'){
        steps }
        echo "echo !"
    }
}