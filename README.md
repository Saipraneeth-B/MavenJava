pipeline {
    agent any
    tools{
        maven 'MAVEN-HOME'
    }
    stages {
        stage('git repo & clean') {
            steps {
                //bat "rmdir  /s /q mavenjava"
                bat "git clone https://github.com/Saipraneeth-B/MavenJava.git"
                bat "mvn clean -f mavenjava"
            }
        }
        stage('install') {
            steps {
                bat "mvn install -f  mavenjava/pom.xml" 
            }
        }
        stage('test') {
            steps {
                bat "mvn test -f mavenjava/pom.xml"
            }
        }
        stage('package') {
            steps {
                bat "mvn package -f mavenjava/pom.xml"
            }
        }
    }
}
