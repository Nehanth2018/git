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
        stage(artifact){
            steps{
                archiveArtifacts 'target/junit-4.13-SNAPSHOT.jar'
            }
        }
        stage(mail){
            steps{
                mail bcc: '', body: '''Hi,
Your build is sucess''', cc: 'vgangarapu@verinon.com', from: '', replyTo: '', subject: 'Build sucess', to: 'mohanreddi88@gmail.com'
            }
        }
	stage('upload') {
           steps {
              script { 
                 def server = Artifactory.server 'Artifactory'
                 def uploadSpec = """{
                    "files": [{
                       "pattern": "/var/lib/jenkins/workspace/Pipelineproject 1/target/junit-4.13-SNAPSHOT.jar",
                       "target": "Test/"
                    }]
                 }"""

                 server.upload(uploadSpec) 
               }
            }
        }
        stage(sonar) {
            steps('SonarQube analysis') {
                withSonarQubeEnv('mysonar') {
			sh 'mvn clean package sonar:sonar'                   
                }
                
            }
        }
    } 
}
