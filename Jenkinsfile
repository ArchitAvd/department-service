pipeline{
    agent any
    tools{
        maven 'my-maven'
        jdk 'my-jdk'
    }
    stages{
        stage('Clone'){
            steps{
                git url:'https://github.com/ArchitAvd/department-service',branch:'master'
            }
        }
        stage('Build'){
            steps{
                bat "mvn clean install -DskipTests"
            }
        }
        stage('Test'){
            steps{
                bat "mvn test"
            }
        }
        stage('Deploy'){
            steps{
                bat "docker rm -f my-dept-container"
                bat "docker rmi -f my-dept-image"
                bat "docker build -t my-dept-image ."
                bat "docker run -p 8081:8081 -d --name my-dept-container my-dept-image"
            }
        }
    }
}