pipeline{

    agent any 
 
      stages{
 
              stage('Checkout GitHubproject'){
	  
	               steps{
	   
	                  checkout changelog: false, poll: false, scm: [$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[credentialsId: 'Gitpwd', url: 'https://github.com/kapiljain2808/simple-maven.git']]]
	  
	                    }
	
	          }
	
	           stage('Build Maven ') {
	                steps{
		
		                 sh 'mvn -B -DskipTests clean package'
		
		                   }
	}
	
	          stage('Build Docker image')
	               {
	                 steps
	                    {
	                        script{
	
	                           sh 'docker build -t kapil2808/simple-maven .'
	
	                              }
	                    }
	
	               }
	
 
	           stage('Push  Docker image') {
	                  steps
	                     {
	                        script{
		
		
		                             withCredentials([string(credentialsId: 'dockerhubpwd', variable: 'dockerpwd')]) {
            
			                           sh 'docker login -u kapil2808 -p ${dockerpwd}'
			                           sh 'docker push  kapil2808/simple-maven'
			
                       }
	
	                 }
	}
	
	}
 
 
 
 }


}
