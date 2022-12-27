node
{
     def mavenhome = tool name: "maven3.8.5"
    stage('checkoutcode')
    {
         git branch: 'development', credentialsId: '1152c42f-f854-4c8e-ab18-c6bd130cc02b', url: 'https://github.com/giriskht7896/maven-web-application-warfile.git'

    }
       //git close
         stage('build package')
    {

        sh"$mavenhome/bin/mvn clean package"
    }
      //maven close

    stage('sonarqube report')
    {
      sh"$mavenhome/bin/mvn sonar:sonar"
    }
    //sonarqube close
    stage('upload to nexus')
    {
        sh"$mavenhome/bin/mvn deploy"
    }
    //nexus close
      stage('deploy to tomcat')
    {
        sshagent(['0715a91b-8164-449a-b5af-5343033e0302']) 
        {
         sh"scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@3.111.40.155:/opt/apache-tomcat-9.0.70/webapps"
        }
    }
    
} //node close
