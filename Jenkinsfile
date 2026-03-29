pipeline{
 tools{
        jdk 'JAVA_HOME_DOCKER'
        maven 'M2_HOME_DOCKER'
    }
      agent { label 'deployslave' }
	  stages{
	  
	  stage("checkout"){
	   steps{
	   git 'https://github.com/tycoonvirat-dot/webapp.git'
	   }
	                  }
	
	   stage("compile"){
	    steps{
		 sh 'mvn compile'
		}
		}
       stage("test"){
	    steps{
		 sh 'mvn test'
		}
		}
       stage("package"){
	    steps{
		 sh 'mvn clean package'
                 sh "mv target/*.war target/myweb.war"

		}
		}
   stage("deploy"){
	   steps{

      sshagent(['docker']){

	        sh """
                 
            scp -o StrictHostKeyChecking=no target/myweb.war ec2-user@65.2.38.221:/usr/local/tomcat/webapps/

              ssh -o StrictHostKeyChecking=no ec2-user@65.2.38.221 "docker cp /tmp/myweb.war tomcat:/usr/local/tomcat/webapps/"
               ssh -o StrictHostKeyChecking=no ec2-user@65.2.38.221 "docker restart tomcat"
            
          
          """

}

	   
		}
		  
	  }
// stage(backup)
// 		  {
//   steps{

// 	  nexusArtifactUploader artifacts: [[artifactId: 'idream-it-solutions', classifier: '', file: 'target/myweb.war', type: '.war']], credentialsId: 'nexus', groupId: 'com.idream.webapp', nexusUrl: '13.204.79.196:8081', nexusVersion: 'nexus3', protocol: 'http', repository: 'repoR', version: '1.1'
//   }
	
// }

	}
	}
