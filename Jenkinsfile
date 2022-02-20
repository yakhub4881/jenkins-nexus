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
              checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/yakhub4881/jenkins-nexus.git']]])
            }
        }
        stage ('BUILD')
        {
            steps{
                sh 'mvn clean package'
            }
        }
        stage ('Upload Artifact To Nexus Publisher')
        {
            steps{
                nexusArtifactUploader artifacts: [[artifactId: 'my-app', classifier: '', file: 'target/Hello World-1.0-SNAPSHOT.war', type: 'war']], credentialsId: 'nexus-admin', groupId: 'com.mycompany.app', nexusUrl: '65.2.30.219:8081', nexusVersion: 'nexus2', protocol: 'http', repository: 'maven-central-repo', version: '1.0-SNAPSHOT'
            }
        }
    }

} 
