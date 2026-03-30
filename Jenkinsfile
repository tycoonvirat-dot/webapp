pipeline{
 tools{
        jdk 'JAVA_HOME_DEPLOY'
        maven 'M2_HOME_DEPLOY'
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
        sshagent(['docker']) {
            sh """
            ssh -o StrictHostKeyChecking=no ec2-user@3.110.83.113 "

            # Copy WAR
            mkdir -p /home/ec2-user/app
            exit
            "

            scp -o StrictHostKeyChecking=no target/myweb.war ec2-user@3.110.83.113:/home/ec2-user/app/

            ssh -o StrictHostKeyChecking=no ec2-user@3.110.83.113 "

            cd /home/ec2-user/app

            # Build Docker image
            docker build -t myapp .

            # Stop old container
            docker stop myapp || true
            docker rm myapp || true

            # Run new container
            docker run -d -p 8081:8080 --name myapp myapp
            "
            """
        }
    }
}
		stage(backup)
		  {
 steps{

nexusArtifactUploader artifacts: [[artifactId: 'idream-it-solutions', classifier: '', file: 'target/myweb.war', type: '.war']], credentialsId: 'nexus', groupId: 'com.idream.webapp', nexusUrl: '3.110.83.113:8082', nexusVersion: 'nexus3', protocol: 'http', repository: 'repoR', version: '1.1'
 }
	
 }

	}
	}
