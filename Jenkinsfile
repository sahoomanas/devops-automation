pipeline{
	agent any
	tools{
	  maven 'maven_3_9_8'
	}
	stages{
	    stage('Build Maven'){
	        steps{
	            checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/sahoomanas/devops-automation']])
	            sh 'mvn clean install'
	        }
	    }
	    stage('Build docker image'){
	        steps{
	            script{
	                sh 'docker build -t sahoomanaskumar/devops-integration .'
	            }
	        }
	    }
	    stage('Push image to Docker Hub'){
	        steps{
	            script{

                     withCredentials([string(credentialsId: 'dockerhub-pwd', variable: 'dockerhubpwd')]) {
    	                def registry_url = "registry.hub.docker.com/"
                        sh 'docker login -u sahoomanaskumar -p ${dockerhubpwd}'
                         sh 'docker push sahoomanaskumar/devops-integration'
                    }
	            }
	        }
	    }
	}
}