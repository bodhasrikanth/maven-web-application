node
{
    def mavenHome = tool name:"maven3.6.3"
    stage('Checkout')
    {
        git credentialsId: '0ee98b38-daa8-4e34-8653-9d856b6a955c', url: 'https://github.com/bodhasrikanth/maven-web-application.git'
    }
    stage('Build')
    {
    sh "${mavenHome}/bin/mvn package"
    }
     stage('ExecutesonarqubeReport')
    {
    sh "${mavenHome}/bin/mvn sonar:sonar"
    }
     stage('ExecuteNexus')
    {
    sh "${mavenHome}/bin/mvn deploy"
    }
    stage('Deploy')
    {
        sshagent(['661bd8c9-8db7-44aa-a039-dd93f598197d']) 
        {
            sh "scp -o StrictHostKeyChecking=no  target/maven-web-application.war  ec2-user@13.235.104.51:/opt/apache-tomcat-9.0.70/webapps/"
    }
    }
}
