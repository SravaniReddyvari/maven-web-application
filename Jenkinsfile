node
{
    def Maven = tool name: "maven_3.6.2";
	stage('Checkoutcode')
	{
	git branch: 'development', credentialsId: '078ef4c7-7c44-49b2-8084-7ab3479a9eb6', 
	url: 'https://github.com/SravaniReddyvari/maven-web-application.git'
	}
	
	stage('build')
	{
	sh "${Maven}/bin/mvn clean package"
	}
	
	stage('ExecuteSonarQube report')
	{
	sh "${Maven}/bin/mvn clean sonar:sonar"
	}
	
	stage('UploadArtifactIntoNexus')
	{
	sh "${Maven}/bin/mvn clean deploy"
	}
	
    stage('DeployIntoTomcat')
	{
	sshagent(['71d8e153-747a-4a11-8ad7-480b7d9b4489']) {
    sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@3.109.200.163:/opt/apache-tomcat-9.0.53/webapps"
	}
	}
	
}
