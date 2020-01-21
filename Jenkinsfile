pipeline {
    agent {
        docker {
            image 'maven:3-alpine'
            args '-v /root/.m2:/root/.m2'
        }
    }
    stages {
        stage('Build') {
            steps {
                sh 'mvn -B -DskipTests clean package'
                 
            }
        }
        
        stage('Test') {
            steps {
                sh 'mvn test'
            }
            post {
                always {
                  junit 'target/surefire-reports/*.xml'
                }
            }
        }
        stage('Test Analysis') {
        steps {
            sh 'mvn cobertura:cobertura'
        }
        post {
            always {
              cobertura coberturaReportFile: 'target/site/cobertura/coverage.xml'
            }
        }
    }
    }
}
