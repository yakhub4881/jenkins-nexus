pipeline {
    agent any
    stages
    {
        stage ('Checkout From SCM')
        {
            steps
            {
                checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/yakhub4881/jenkins-nexus.git']]])
            }
        }
        stage ('Build')
        {
            steps{
                sh 'mvn clean package'
            }
        }
    }
}