pipeline{
    agent {
        docker {
            image 'maven:3-alpine'
            args '-v /root/.m2/:/root/.m2'
        }
    }
    stages {
        stage('Build'){
            steps {
                sh 'mvn -B -DskipTest clean package'
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test'
            }
            post {
                always {
                    junit 'target/surefire-report/*.xml'
                }
            }
        }
        stage('Deliver') {
            steps {
                sh './jenkins/secript/deliver.sh'
            }
        }
    }
}
