node
{
    def mavenhome= tool name: "maven3.8.2"
    stage('getcode')
    {
        git branch: 'development', url: 'https://github.com/rituja12/maven-web-application.git'
    }
    stage('build')
    {
        sh "${mavenhome}/bin/mvn clean package"
    }
    stage('generatesonarreport')
    {
        sh "${mavenhome}/bin/mvn clean sonar:sonar"
    }
    stage('uploadartifact')
    {
        sh "${mavenhome}/bin/mvn clean deploy"
    }
    stage('deployintomcat')
    {
        sshagent(['496aa813-35ab-4e12-bf26-45dd37a37b6b'])
        {
        sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@52.66.255.14:/opt/apache-tomcat-9.0.53/webapps"
        }
        
    stage('sendEmail')
    {
        emailext body: 'build over', subject: 'build over', to: 'ninave.rituj@gmail.com'
    }
    }
    
}
    
    
    
    
    
    
    
    
    
    
    
    
    
    
