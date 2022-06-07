pipeline {
    agent none
    triggers {
        cron('0 * * * *')
    }
    stages {
        stage('CleanWorkspace') {
            agent { label 'mvn3.8.5' }
            steps {
                cleanWs()
            }
        }
        stage('SCM Checkout') {
            agent { label 'master' }
            steps{
            git url: 'https://github.com/Manojkumarpolaka/python-sample-vscode-flask-tutorial.git', branch: "master"
            }
        }
        stage('Build') {
            agent { label 'mvn3.8.5' }
            steps{
                withSonarQubeEnv(installationName: 'SONAR', envOnly: true, credentialsId: 'SONAR') {
                    sh 'python3 -m pip install --upgrade pip setuptools wheel'
                    sh 'pip install -r requirements.txt'
                    sh 'python3 -m pip install flake8'
                }
            }
        }
    }
}
