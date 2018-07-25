pipeline{
    agent any
    stages{
        stage(git){
            steps{
                git 'https://github.com/junit-team/junit4.git'
            }
        }
        stage(mvn){
            steps{
                sh 'mvn clean install'
            }
        }
        stage(copy){
            steps{
                sh 'cp target/*.jar /tmp'
            }
        }
        stage(junit){
            steps{
                junit 'target/surefire-reports/*.xml'
            }
        }
        
    }
}
