pipeline{
    agent any
    environment {
        PATH = "$PATH:/usr/share/maven"
    }
    stages
    {
        stage ('Checkout From SCM')
        {
            steps
            {
              checkout([$class: 'GitSCM', branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/yakhub4881/javaloginapp.git']]])
            }
        }
        stage ('BUILD')
        {
            steps{
                sh 'mvn clean package'
            }
        }
        stage ('SonarQube Analysis')
        {
            steps{
                withSonarQubeEnv('SonarQube8.9.2') {
                sh 'mvn sonar:sonar'
                }                
            }
        }
        stage ('Upload Artifact To Nexus Publisher')
        {
            steps{
                nexusArtifactUploader artifacts: [[artifactId: 'my-app', classifier: '', file: 'target/Hello World-1.0-SNAPSHOT.war', type: 'war']], credentialsId: 'nexus-admin', groupId: 'com.mycompany.app', nexusUrl: '65.2.30.219:8081', nexusVersion: 'nexus2', protocol: 'http', repository: 'http://65.2.30.219:8081/repository/maven-central-repo/', version: '1.0-SNAPSHOT'
            }
        }
    }
