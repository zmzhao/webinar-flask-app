pipeline {
    agent {
        kubernetes {
            defaultContainer 'jnlp'
            yamlFile 'build.yaml'
        }
    }
    stages {
        stage('Test') {
            steps {
                container('pytest') {
                    dir('app') {
                        sh 'pip install -r requirements.txt'
                        sh 'pytest'
                    }
                }
            }
        }
        stage('Build') {
            steps {
                container('docker-client') {
                    sh 'docker build . -t devops:flask-app'
                }
            }
        }
        stage('Deploy') {
            steps {
                container('docker-client') {
                    sh 'docker run -d -p 5000:5000 devops:flask-app'
                    sh 'docker ps'
                }
            }
        }
    }
}
