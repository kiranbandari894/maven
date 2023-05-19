@Library('cicdlib')_
pipeline{
    agent any
    stages{
        stage('ContinuousDownload'){
           steps{
		       script{
			     try{
				  cicd.getGit('https://github.com/kiranbandari894/maven.git')
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
				    cicd.buildApp()
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
				   cicd.DeployApp("DeclarativePipelines",'172.19.0.3','ubuntu','testingapp')
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
				   cicd.Test('https://github.com/intelliqittrainings/FunctionalTesting.git','DeclarativePipelines','testing')
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
				     cicd.DeployApp("DeclarativePipelines",'172.19.0.4','production','prodapp')
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
