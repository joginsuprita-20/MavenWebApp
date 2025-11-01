pipeline {
    agent any

    tools {
        maven 'Maven'   // Must match the Maven name in Jenkins configuration
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'master', url: 'https://github.com/joginsuprita-20/MavenWebApp.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }

        stage('Deploy to Tomcat') {
            steps {
                echo 'Deploying WAR to Tomcat...'
                sh '''
                    sudo /opt/tomcat/bin/shutdown.sh || true
                    sudo cp target/*.war /opt/tomcat/webapps/MymavenWebApp01.war
                    sudo /opt/tomcat/bin/startup.sh
                '''
            }
        }
    }

    post {
        success {
            echo 'Build and deployment successful!'
        }
        failure {
            echo 'Build failed!'
        }
    }
}

