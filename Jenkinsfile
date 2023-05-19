pipeline{
    agent any
    stages{
        stage('ContinuousDownload'){
           steps{
		       script{
			     try{
				   git 'https://github.com/kiranbandari894/maven.git'
				 }catch(Exception e1){
				    mail bcc: '', body: 'Jenkina Download Job failed....', cc: '', from: '', replyTo: '', subject: 'Jenkins Download Job Failed', to: 'kiranbandari894@gmail.com'
				 } 
			   }
                
           }
        }
        stage('ContinuousBuild'){
           steps{
               script{
			     try{
				    sh 'mvn package'
				 }catch(Exception e2){
				   mail bcc: '', body: '''Jenkins Build Faild please check logs..

				   Thanks & Regards 
				   Jenkins''', cc: '', from: '', replyTo: '', subject: 'Build Fail ', to: 'kiranbandari894@gmail.com'				 
				 }
			    
			   }  
           }
        }
        stage('ContinuousDeployment'){
           steps{
             script{
			    try{
				   sh 'scp /var/jenkins_home/workspace/DeclarativePipelines/webapp/target/webapp.war  ubuntu@172.19.0.3:/usr/local/tomee/webapps/mytestapp.war'
				   mail bcc: '', body: '''Jenkins Testing server Deployment Success.

				   Thanks & Regards 
                   Jenkins''', cc: '', from: '', replyTo: '', subject: 'Jenkins Testing server Deployment Success', to: 'kiranbandari894@gmail.com'
				}catch(Exception e3){
				   mail bcc: '', body: '''Jenkins Testing server Deployment Fail Please check logs.

                   Thanks & Regards 
                   Jenkins''', cc: '', from: '', replyTo: '', subject: 'Jenkins Testing server Deployment Fail', to: 'kiranbandari894@gmail.com'
				
				}
			 }   
           }
        }
        stage('ContinuousTesting'){
            steps{
              script{
			    try{
				  git 'https://github.com/intelliqittrainings/FunctionalTesting.git'
                  sh 'java -jar /var/jenkins_home/workspace/DeclarativePipelines/testing.jar'
				  mail bcc: '', body: '''Jenkins Testing is Success 

				  Thanks & Regards 
                  Jenkins''', cc: '', from: '', replyTo: '', subject: 'Jenkins Testing Success', to: 'kiranbandari894@gmail.com'
				}catch(Exception e4){
				  mail bcc: '', body: '''Jenkins Testing is Failed Please check logs

				  Thanks & Regards 
				  Jenkins''', cc: '', from: '', replyTo: '', subject: 'Jenkins Testing Fail', to: 'kiranbandari894@gmail.com'
				}
			  }
            }
        }
		stage('ContinuousDelivery'){
		    steps{
			   script{
			     try{
				     sh 'scp /var/jenkins_home/workspace/DeclarativePipelines/webapp/target/webapp.war  prodution@172.19.0.4:/usr/local/tomee/webapps/myprodapp.war'
					 mail bcc: '', body: '''Hi,Your Deployment job has run successfull and Deployment has done successful. Thanks & regards, Jenkins Dashboard''', cc: '', from: '', replyTo: '', subject: 'Deployment Job Successful', to: 'kiranbandari894@gmail.com'
				 }
				 catch(Exception e5){
				     mail bcc: '', body: 'Jenkins Production Delivery Failed', cc: '', from: '', replyTo: '', subject: 'Jenkins Production Delivery Failed', to: 'kiranbandari894@gmail.com'
				 }
			   }
			}
		}
     
    }
 
}
