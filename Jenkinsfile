pipeline{
    agent any
    stages{
        stage('ContinuousDownload'){
           steps{
                git 'https://github.com/kiranbandari894/maven.git'
           }
        }
        stage('ContinuousBuild'){
           steps{
                sh 'mvn package'
           }
        }
        stage('ContinuousDeployment'){
           steps{
                sh 'scp /var/jenkins_home/workspace/DeclarativePipelines/webapp/target/webapp.war  ubuntu@172.18.0.2:/usr/local/tomee/webapps/mytestapp.war'
           }
        }
        stage('ContinuousTesting'){
            steps{
                git 'https://github.com/intelliqittrainings/FunctionalTesting.git'
                sh 'java -jar /var/jenkins_home/workspace/DeclarativePipelines/testing.jar'
            }
        }
     
    }
	post{
		  success{
		    deploy adapters: [tomcat9(credentialsId: '24845a25-1540-433a-bcae-40d87d61b004', path: '', url: 'http://172.18.0.4:8080/')], contextPath: 'myprodapp', war: '**/*.war'
            
			mail bcc: '', body: '''Hi,Your Deployment job has run successfull and Deployment has done successful. Thanks & regards, Jenkins Dashboard''', cc: '', from: '', replyTo: '', subject: 'Deployment Job Successful', to: 'kiranbandari894@gmail.com'
		  }
		  failure{
			mail bcc: '', body: '''Hi, Your Deployment job has  fail Please check logs Thanks & regards, Jenkins Dashboard''', cc: '', from: '', replyTo: '', subject: 'Deployment Job Failed', to: 'kiranbandari894@gmail.com'
		  }
	}
}
