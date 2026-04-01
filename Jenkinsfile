pipeline{
 tools{
        jdk 'JAVA_HOME_WINDOW'
        maven 'M2_HOME_WINDOW'
    }
     agent any
	  
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
//    stage("deploy"){
// 	   steps{

//       sshagent(['docker']) {
//     sh '''
//     scp -o StrictHostKeyChecking=no target/myweb.war ec2-user@3.111.147.110:/home/ec2-user/tomcat1/webapps/

//     ssh ec2-user@3.111.147.110 "cd /home/ec2-user/tomcat1/bin && ./shutdown.sh || true"

//     ssh ec2-user@3.111.147.110 "cd /home/ec2-user/tomcat1/bin && ./startup.sh"
//     '''
// }

	   
// 		}
		  
// 	  }

// stage("backup")
// // 		  {
// //   steps{

// // 	  nexusArtifactUploader artifacts: [[artifactId: 'idream-it-solutions', classifier: '', file: 'target/myweb.war', type: 'war']], credentialsId: 'nexus', groupId: 'com.idream.webapp', nexusUrl: '3.110.167.8:8080/nexus/', nexusVersion: 'nexus2', protocol: 'http', repository: 'repoR', version: '1.1'
	  
// //   }
	
// // }
	}
	}
