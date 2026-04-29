pipeline
{
	agent any
	tools
	{
	maven "maven"
	}
	stages
	{
	 	stage("git checkout")
	 	{
	 		steps
	 		{
	 			git 'https://github.com/FromKKFunda/maven-webapplication-project-kkfunda.git'
	 		}
	 	}
	 	stage ("build artiface")
	 	{
	 		steps
	 		{
	 			sh "mvn clean package"
	 		}
	 		
	 	}
	 	stage("sonar Qube report generate")
	 	{
	 		steps
	 		{
	 			sh "mvn sonar:sonar"
	 		}
	 	}
	 	stage("artiface to nexus")
	 	{
	 		steps
	 		{
	 			sh "mvn clean deploy"
	 		}
	 	}
	 	stage("deploy to tomcat")
	 	{
	 		steps
	 		{
	 			sh """
	    curl -v -u "manikantha:Mani52@1" \
	    "http://3.110.144.137:8080//manager/text/undeploy?path=/maven-web-application"

	    curl -v -u "manikantha:Mani52@1" \
	    --upload-file target/maven-web-application.war \
	    "http://3.110.144.137:8080//manager/text/deploy?path=/maven-web-application"
	    """
	 		}
	 	}
		stage("biuld dev")
	 	{
	 		steps
	 		{
	 			build job: "dev"
	 		}
	 	}
	}
}
